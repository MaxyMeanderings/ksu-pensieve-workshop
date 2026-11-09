# Pensieve AWS source excerpts

Captured 2026-11-09 from secure-sharing. Source inspection only; not a fresh runtime result. Line numbers below refer to the original files. Full-file hashes identify captured content.


## src/aws-team-store.ts

SHA-256: 83fe210b53fa029c930d7ebbade4571026862c09a208b969228cd4682af4b55d


### src/aws-team-store.ts:10

```text
10: export interface AwsVectorRecord {key:string;poolId:string;memoryId:string;revision:string;model:string;vector:number[]}
11: export interface AwsVectorIndex {upsert(records:AwsVectorRecord[]):Promise<void>;query(input:{poolId:string;model:string;vector:number[];limit:number}):Promise<{memoryId:string;revision:string;score:number}[]>}
12: export interface AwsTeamOptions {vectors?:AwsVectorIndex;prepareSnapshot?:(input:ShareInput)=>Promise<{snapshot:Snapshot;actions:AwsWrite[]}>;now?:()=>number}
```


### src/aws-team-store.ts:26

```text
26: export class AwsTeamStore implements TeamRepository {
27:  readonly indexingMode='queued' as const;
28:  private readonly now:()=>number;
29:  private constructor(readonly db:AwsDatabase,readonly sourceServer:string,readonly options:AwsTeamOptions){this.now=options.now??Date.now;}
30:  static async open(db:AwsDatabase,options:AwsTeamOptions={}):Promise<AwsTeamStore>{let meta=await db.get('SYSTEM','ISSUER');if(!meta){try{await db.put({pk:'SYSTEM',sk:'ISSUER',value:randomUUID()},'attribute_not_exists(pk)');}catch(e){if(!conditionalFailure(e))throw e;}meta=await db.get('SYSTEM','ISSUER');}if(typeof meta?.value!=='string')throw Error('Missing issuer');return new AwsTeamStore(db,meta.value,options);}
31:  async close():Promise<void>{}
32:  private async user(id:string){const row=await this.db.get<UserRow>(userKey(id),'META');if(!row?.active)throw new TeamAccessError(401,'Unauthorized identity');return row;}
33:  private userUsed(row:UserRow):AwsWrite{return this.db.putAction({...row,used:true,version:row.version+1},'version=:v AND active=:active',{':v':row.version,':active':true});}
34:  private userCheck(row:UserRow){return this.db.check(row.pk,row.sk,'version=:v AND active=:active',{':v':row.version,':active':true});}
35:  private async access(actor:string,pool:string,write=false){const user=await this.user(actor);const rows=await this.db.batchGet([{pk:poolKey(pool),sk:'META'},{pk:poolKey(pool),sk:`MEMBER#${actor}`}]);const p=rows.find(x=>x.sk==='META') as PoolRow|undefined,m=rows.find(x=>x.sk.startsWith('MEMBER#')) as MemberRow|undefined;if(!p||!m)throw new TeamAccessError(404,'Pool unavailable');if(write&&m.role==='reader')throw new TeamAccessError(403,'Writer authorization required');return {user,p,m};}
36:  private checks(a:Awaited<ReturnType<AwsTeamStore['access']>>,used=true):AwsWrite[]{return [used?this.userUsed(a.user):this.userCheck(a.user),this.db.check(a.m.pk,a.m.sk,'version=:v',{':v':a.m.version})];}
```


### src/aws-team-store.ts:50

```text
50:  async putMemory(actor:string,pool:string,memory:Memory){const r=await this.putMemories(actor,pool,[memory]);return {id:memory.id,created:r.imported===1};}
51:  async putMemories(actor:string,pool:string,memories:Memory[],provenance?:MemoryProvenance[]){
52:   if(!Array.isArray(memories)||!memories.length||memories.length>10000)throw Error('Invalid memory batch');memories.forEach(validateMemoryRecord);const unique=new Map<string,Memory>();for(const m of memories){if(unique.has(m.id)&&canonical(unique.get(m.id))!==canonical(m))throw Error(`Conflicting content for memory ${m.id}`);unique.set(m.id,m);}const ids=[...unique.keys()],origins=provenance?validateProvenance(provenance,new Set(ids)):[];
53:   const byMemory=new Map<string,MemoryProvenance[]>();for(const origin of origins){const list=byMemory.get(origin.memoryId)??[];list.push(origin);byMemory.set(origin.memoryId,list);}
54:   const a=await this.access(actor,pool,true),batchId=randomUUID(),now=this.now(),leaseUntil=now+15*60*1000,marker:BatchRow={pk:batchKey(batchId),sk:'META',kind:'index-batch',state:'staging',poolId:pool,actor,created:now,indexState:'pending',indexVersion:0};
55:   await this.db.transact([...this.checks(a,false),this.db.putAction({...a.p,lease:batchId,leaseUntil,version:a.p.version+1},'version=:v AND (attribute_not_exists(leaseUntil) OR leaseUntil < :now)',{':v':a.p.version,':now':now}),this.db.putAction(marker,'attribute_not_exists(pk)'),this.db.putAction({pk:'WORK#INDEX',sk:`PENDING#${batchId}`,batchId},'attribute_not_exists(pk)')]);let imported=0;
56:   try{
57:    const entries=[...unique.values()];for(let offset=0;offset<entries.length;offset+=8){const chunk=entries.slice(offset,offset+8),existing=await this.db.batchGet<MemoryRow>(chunk.map(m=>({pk:poolKey(pool),sk:`MEMORY#${m.id}`}))),visible=await this.committed(existing),visibleIds=new Set(visible.map(m=>m.memory.id));
58:     const originBatches=await this.db.batchGet<BatchRow>(existing.filter(r=>r.originBatch).map(r=>({pk:batchKey(r.originBatch!),sk:'META'}))),originOk=new Set(originBatches.filter(b=>b.state==='committed').map(b=>b.pk));const actions:AwsWrite[]=[this.db.check(poolKey(pool),'META','lease=:lease AND leaseUntil>:now',{':lease':batchId,':now':this.now()})];
59:     for(const memory of chunk){const old=existing.find(r=>r.memory.id===memory.id),live=old&&visibleIds.has(memory.id);if(live&&canonical(old.memory)!==canonical(memory))throw Error(`Conflicting content for memory ${memory.id}`);
60:      const base=live?[...old.origins,...(old.originBatch&&originOk.has(batchKey(old.originBatch))?old.pendingOrigins??[]:[])]:[];
61:      const extra=(byMemory.get(memory.id)??[]).map(p=>({...p,verification:'unverified-import' as const}));const merged=[...new Map([...base,...extra].map(p=>[canonical([p.sourceServer,p.poolId,p.memoryId,p.contributorId,p.createdAt]),p])).values()];
62:      const row:MemoryRow=live?{...old,pendingOrigins:merged,originBatch:batchId,origins:[],version:old.version+1}:{pk:poolKey(pool),sk:`MEMORY#${memory.id}`,memory,revision:hash(canonical(memory)),contributorId:actor,contributorName:a.user.name,createdAt:new Date(now).toISOString(),batchId,origins:merged,version:(old?.version??0)+1};
63:      // Keep prior provenance visible while a new publication is staged.
64:      if(live)row.origins=base;
65:      size(row);actions.push(this.db.putAction(row,old?'version=:v':'attribute_not_exists(pk)',old?{':v':old.version}:undefined));
66:      if(!live){imported++;actions.push(this.db.putAction({pk:batchKey(batchId),sk:`JOB#${memory.id}`,kind:'index-job',poolId:pool,memoryId:memory.id,revision:row.revision,state:'pending'}));}
67:     }await this.db.transact(actions);
68:    }
69:    const final=await this.access(actor,pool,true);await this.db.transact([...this.checks(final),this.db.putAction({...final.p,leaseUntil:0,lease:'',version:final.p.version+1},'lease=:lease AND leaseUntil>:now',{':lease':batchId,':now':this.now()}),{Put:{TableName:this.db.table,Item:{...marker,state:'committed'},ConditionExpression:'#state=:staging',ExpressionAttributeNames:{'#state':'state'},ExpressionAttributeValues:{':staging':'staging'}}}]);
70:    return {imported,ids};
71:   }catch(error){const current=await this.db.get<BatchRow>(marker.pk,'META');if(current?.state==='committed')return {imported,ids};try{await this.db.transact([{Put:{TableName:this.db.table,Item:{...marker,state:'failed'},ConditionExpression:'#state=:staging',ExpressionAttributeNames:{'#state':'state'},ExpressionAttributeValues:{':staging':'staging'}}}]);}catch{/* original failure remains primary */}try{const p=await this.db.get<PoolRow>(poolKey(pool),'META');if(p?.lease===batchId)await this.db.put({...p,lease:'',leaseUntil:0,version:p.version+1},'lease=:lease',{':lease':batchId});}catch{/* lease expires */}throw error;}
72:  }
73:  async listMemoryPage(actor:string,pool:string,options:{limit?:number;cursor?:string}={}):Promise<MemoryPage>{await this.access(actor,pool);const page=await this.db.query<MemoryRow>(poolKey(pool),pageOptions(options,'MEMORY#'));const rows=await this.committed(page.items);await this.access(actor,pool);return {memories:rows.map(r=>({memory:r.memory,contributorId:r.contributorId,createdAt:r.createdAt})),...(page.cursor?{nextCursor:page.cursor}:{})};}
74:  async listMemories(actor:string,pool:string):Promise<TeamMemory[]>{const result:TeamMemory[]=[];let cursor:string|undefined;do{const p=await this.listMemoryPage(actor,pool,{limit:100,cursor});result.push(...p.memories);cursor=p.nextCursor;if(cursor&&result.length>=10000)throw Error('Use paginated memory listing');}while(cursor);return result;}
75:  private async selected(actor:string,pool:string,ids:string[]){await this.access(actor,pool);if(!Array.isArray(ids)||ids.length>10000||ids.some(id=>!(/^[a-f0-9]{64}$/).test(id)))throw Error('Invalid memory selection');const unique=[...new Set(ids)],rows=await this.committed(await this.db.batchGet<MemoryRow>(unique.map(id=>({pk:poolKey(pool),sk:`MEMORY#${id}`}))));const map=new Map(rows.map(r=>[r.memory.id,r]));if(unique.some(id=>!map.has(id)))throw new TeamAccessError(404,'Memory unavailable');await this.access(actor,pool);return unique.map(id=>map.get(id)!);}
76:  async getMemories(actor:string,pool:string,ids:string[]){return (await this.selected(actor,pool,ids)).map(r=>r.memory);}
77:  async exportBundle(actor:string,pool:string,ids:string[]):Promise<Bundle>{if(!ids?.length)throw Error('Select at least one memory explicitly');const rows=await this.selected(actor,pool,ids),batches=await this.db.batchGet<BatchRow>(rows.filter(r=>r.originBatch).map(r=>({pk:batchKey(r.originBatch!),sk:'META'}))),ok=new Set(batches.filter(b=>b.state==='committed').map(b=>b.pk));const provenance:MemoryProvenance[]=[];for(const r of rows){provenance.push({memoryId:r.memory.id,contributorId:r.contributorId,contributorName:r.contributorName,poolId:pool,createdAt:r.createdAt,sourceServer:this.sourceServer,verification:'source-server'},...(r.originBatch&&ok.has(batchKey(r.originBatch))?r.pendingOrigins??r.origins:r.origins));}return {format:'pensieve/v1',createdAt:new Date(this.now()).toISOString(),memories:rows.map(r=>r.memory),provenance};}
```


### src/aws-team-store.ts:99

```text
99:   ]);return true;
100:  }
101:  async processIndexBatch(batchId:string,provider:EmbeddingProvider,options:{limit?:number}={}):Promise<{processed:number;done:boolean}>{
102:   const batch=await this.db.get<BatchRow>(batchKey(batchId),'META');if(!batch||batch.state!=='committed')return {processed:0,done:true};if(batch.indexState==='ready'||batch.indexState==='blocked'){await this.db.delete('WORK#INDEX',`PENDING#${batchId}`);return {processed:0,done:true};}
103:   try {
104:   if(await this.blockInactiveIndexActor(batch))return {processed:0,done:true};
105:   if(!this.options.vectors)throw Error('Vector index unavailable');if(batch.model&&batch.model!==provider.identity)throw Error('Index model changed');await this.access(batch.actor,batch.poolId,true);
106:   const limit=options.limit??16;if(!Number.isInteger(limit)||limit<1||limit>32)throw Error('Index batch limit must be 1..32');const jobs=batch.reindex?await this.db.query<MemoryRow>(poolKey(batch.poolId),{prefix:'MEMORY#',after:batch.cursor||undefined,limit}):await this.db.query<JobRow>(batch.pk,{prefix:'JOB#',after:batch.cursor||undefined,limit});const rows=batch.reindex?await this.committed(jobs.items as MemoryRow[]):jobs.items.length?await this.selected(batch.actor,batch.poolId,(jobs.items as JobRow[]).map(j=>j.memoryId)):[];
107:   const receiptKey=(id:string)=>`INDEX#${hash(provider.identity)}#${id}`;
108:   const receipts=await this.db.batchGet(rows.map(r=>({pk:poolKey(batch.poolId),sk:receiptKey(r.memory.id)})));const current=new Map(receipts.map(r=>[r.sk,r.revision]));const pending=rows.filter(r=>current.get(receiptKey(r.memory.id))!==r.revision);
109:   const vectors=pending.length?await provider.embed(pending.map(r=>r.memory.text),'document'):[];if(vectors.length!==pending.length)throw Error('Embedding response count mismatch');vectors.forEach(validateVector);const dim=vectors[0]?.length;if(vectors.some(v=>v.length!==dim))throw Error('Embedding dimension changed');await this.access(batch.actor,batch.poolId,true);
110:   const records=pending.map((r,i)=>({key:hash(JSON.stringify([batch.poolId,r.memory.id,r.revision,provider.identity])),poolId:batch.poolId,memoryId:r.memory.id,revision:r.revision,model:provider.identity,vector:vectors[i]}));if(records.length)await this.options.vectors.upsert(records);
111:   const a=await this.access(batch.actor,batch.poolId,true);const updated={...batch,indexState:jobs.cursor?'pending':'ready',cursor:jobs.cursor??'',indexVersion:(batch.indexVersion??0)+1};const actions=[...this.checks(a,false),this.db.putAction(updated,'indexVersion=:v',{':v':batch.indexVersion??0})];
112:   for(const r of pending){actions.push(this.db.check(r.pk,r.sk,'revision=:revision AND (attribute_not_exists(deleted) OR deleted=:no)',{':revision':r.revision,':no':false}),this.db.putAction({pk:poolKey(batch.poolId),sk:receiptKey(r.memory.id),revision:r.revision,model:provider.identity}));}
113:   if(!jobs.cursor)actions.push({Delete:{TableName:this.db.table,Key:{pk:'WORK#INDEX',sk:`PENDING#${batchId}`}}});await this.db.transact(actions);return {processed:rows.length,done:!jobs.cursor};
114:   }catch(error){if(await this.blockInactiveIndexActor(batch))return {processed:0,done:true};throw error;}
```


### src/aws-team-store.ts:139

```text
139:  async search(actor:string,pool:string,query:string,provider:EmbeddingProvider,limit=8):Promise<Hit[]>{await this.access(actor,pool);bounded(query,'query',4000);if(!Number.isInteger(limit)||limit<1||limit>50)throw Error('Limit must be 1..50');if(!this.options.vectors)throw Error('Vector index unavailable');const vectors=await provider.embed([query],'query');if(vectors.length!==1)throw Error('Invalid query embedding');validateVector(vectors[0]);const hits=await this.options.vectors.query({poolId:pool,model:provider.identity,vector:vectors[0],limit:Math.min(100,limit*2)});const rows=await this.committed(await this.db.batchGet<MemoryRow>(hits.map(h=>({pk:poolKey(pool),sk:`MEMORY#${h.memoryId}`}))));const map=new Map(rows.map(r=>[r.memory.id,r]));await this.access(actor,pool);const seen=new Set<string>();return hits.flatMap(h=>{const row=map.get(h.memoryId);if(!row||row.revision!==h.revision||!Number.isFinite(h.score)||seen.has(h.memoryId))return [];seen.add(h.memoryId);return [{...row.memory,score:h.score}];}).slice(0,limit);}
```


## src/aws-db.ts

SHA-256: e8fadd4963a49895725762f193e6fbf48fef5f1711084214aabf4a05107b9112


### src/aws-db.ts:6

```text
6: export class AwsDatabase {
7:  constructor(readonly client:DynamoDBDocumentClient,readonly table:string){if(!table)throw Error('DynamoDB table required');}
8:  async get<T extends AwsItem=AwsItem>(pk:string,sk:string):Promise<T|undefined>{const r=await this.client.send(new GetCommand({TableName:this.table,Key:{pk,sk},ConsistentRead:true}));return r.Item as T|undefined;}
9:  async put(item:AwsItem,condition?:string,values?:Record<string,unknown>):Promise<void>{await this.client.send(new PutCommand({TableName:this.table,Item:item,...(condition?{ConditionExpression:condition}:{}),...(values?{ExpressionAttributeValues:values}:{})}));}
10:  async delete(pk:string,sk:string):Promise<void>{await this.client.send(new DeleteCommand({TableName:this.table,Key:{pk,sk}}));}
11:  async query<T extends AwsItem=AwsItem>(pk:string,options:{prefix?:string;after?:string;limit?:number}={}):Promise<AwsPage<T>>{
12:   const limit=options.limit??50;if(!Number.isInteger(limit)||limit<1||limit>100)throw Error('Query page limit must be 1..100');
13:   const r=await this.client.send(new QueryCommand({TableName:this.table,ConsistentRead:true,KeyConditionExpression:options.prefix?'pk=:pk AND begins_with(sk,:prefix)':'pk=:pk',ExpressionAttributeValues:{':pk':pk,...(options.prefix?{':prefix':options.prefix}:{})},Limit:limit,...(options.after?{ExclusiveStartKey:{pk,sk:options.after}}:{})}));
14:   return {items:(r.Items??[]) as T[],...(r.LastEvaluatedKey?{cursor:String(r.LastEvaluatedKey.sk)}:{})};
15:  }
16:  async batchGet<T extends AwsItem=AwsItem>(keys:AwsKey[]):Promise<T[]>{
17:   const unique=[...new Map(keys.map(k=>[JSON.stringify(k),k])).values()],result:T[]=[];
18:   for(let offset=0;offset<unique.length;offset+=100){let pending=unique.slice(offset,offset+100);for(let attempt=0;pending.length&&attempt<6;attempt++){
19:    const r=await this.client.send(new BatchGetCommand({RequestItems:{[this.table]:{Keys:pending,ConsistentRead:true}}}));result.push(...(r.Responses?.[this.table]??[]) as T[]);pending=(r.UnprocessedKeys?.[this.table]?.Keys??[]) as AwsKey[];
20:    if(pending.length)await new Promise(resolve=>setTimeout(resolve,Math.min(1000,25*2**attempt)));
21:   }if(pending.length)throw Error('DynamoDB batch read incomplete');}return result;
22:  }
23:  async transact(actions:AwsWrite[],token?:string):Promise<void>{if(!actions.length||actions.length>100)throw Error('Transaction must contain 1..100 actions');await this.client.send(new TransactWriteCommand({TransactItems:actions,...(token?{ClientRequestToken:token}:{})}));}
24:  putAction(item:AwsItem,condition?:string,values?:Record<string,unknown>):AwsWrite{return {Put:{TableName:this.table,Item:item,...(condition?{ConditionExpression:condition}:{}),...(values?{ExpressionAttributeValues:values}:{})}};}
25:  check(pk:string,sk:string,condition:string,values?:Record<string,unknown>):AwsWrite{return {ConditionCheck:{TableName:this.table,Key:{pk,sk},ConditionExpression:condition,...(values?{ExpressionAttributeValues:values}:{})}};}
```


## test/aws-storage.test.ts

SHA-256: c93f183cb34070f24bce714f3f62ac045a1573a313d9fb83790f4358e950ca3c


### test/aws-storage.test.ts:20

```text
20: const vectors:AwsVectorIndex={upsert:async()=>{},query:async()=>[]};
21: test('AC1/2/3 DynamoDB repositories publish bounded imports atomically and preserve provenance',{skip:!table},async()=>{
22:  const store=await AwsTeamStore.open(db,{vectors}),alice=await store.createUser('Alice '+randomUUID()),bob=await store.createUser('Bob '+randomUUID());
23:  const pool=await store.createPool(alice.user.id,'Storage canary','shared');assert.equal((await store.authenticate(alice.token)).id,alice.user.id);
24:  await store.grantMember(alice.user.id,pool.id,bob.user.id,'reader');await assert.rejects(store.putMemory(bob.user.id,pool.id,memory('denied')),/Writer/);
25:  const records=Array.from({length:53},(_,i)=>memory('decision '+i)),result=await store.putMemories(alice.user.id,pool.id,records);assert.equal(result.imported,53);
26:  const first=await store.listMemoryPage(alice.user.id,pool.id);assert.equal(first.memories.length,50);assert.ok(first.nextCursor);const second=await store.listMemoryPage(alice.user.id,pool.id,{cursor:first.nextCursor});assert.equal(second.memories.length,3);assert.equal(new Set([...first.memories,...second.memories].map(r=>r.memory.id)).size,53);
27:  assert.equal((await store.putMemories(alice.user.id,pool.id,records)).imported,0);
28:  const added=Array.from({length:20},(_,i)=>memory('staged '+i));await assert.rejects(store.putMemories(alice.user.id,pool.id,[...added,{...records[0],text:'conflict'}]),/Conflicting/);
29:  await assert.rejects(store.getMemories(alice.user.id,pool.id,[added[0].id]),/unavailable/);assert.equal((await store.listMemories(alice.user.id,pool.id)).length,53);
30:  const failed=await db.get(`POOL#${pool.id}`,`MEMORY#${added[0].id}`);assert.equal(await store.cleanupAbandonedBatch(String(failed?.batchId)),16);assert.equal(await store.cleanupAbandonedBatch(String(failed?.batchId)),0);assert.equal(await db.get(`POOL#${pool.id}`,`MEMORY#${added[0].id}`),undefined);const committed=await db.get(`POOL#${pool.id}`,`MEMORY#${records[0].id}`);assert.equal(await store.cleanupAbandonedBatch(String(committed?.batchId)),0);
31:  assert.equal((await store.putMemories(alice.user.id,pool.id,added)).imported,20);
32:  const origin={memoryId:records[0].id,contributorId:'source-author',contributorName:'Source',poolId:'source-pool',createdAt:new Date().toISOString(),sourceServer:'source-server',verification:'source-server' as const};
33:  await store.putMemories(alice.user.id,pool.id,[records[0]],[origin]);await store.putMemories(alice.user.id,pool.id,[records[0]],[origin]);
34:  const bundle=await store.exportBundle(alice.user.id,pool.id,[records[0].id]);assert.equal(bundle.provenance?.filter(p=>p.sourceServer==='source-server').length,1);assert.equal(bundle.provenance?.find(p=>p.sourceServer==='source-server')?.verification,'unverified-import');
35:  await assert.rejects(store.listMemoryPage(alice.user.id,pool.id,{limit:101}),/Page limit/);
```


### test/aws-storage.test.ts:44

```text
44:  const index:AwsVectorIndex={upsert:async records=>{upserts.push(records);},query:async()=>hits};const store=await AwsTeamStore.open(db,{vectors:index});
45:  const user=await store.createUser('Indexer '+randomUUID()),pool=await store.createPool(user.user.id,'Index canary','private'),records=Array.from({length:33},(_,i)=>memory('index '+i));await store.putMemories(user.user.id,pool.id,records);
46:  const row=await db.get(`POOL#${pool.id}`,`MEMORY#${records[0].id}`),batchId=String(row?.batchId);assert.ok(batchId);
47:  await assert.rejects(store.processIndexBatch(batchId,{identity:'test:v1',embed:async()=>{throw Error('provider unavailable');}}),/provider unavailable/);assert.equal(upserts.length,0);
48:  const first=await store.processIndexBatch(batchId,provider);assert.equal(first.processed,16);assert.equal(first.done,false);await store.processIndexBatch(batchId,provider);assert.equal((await store.processIndexBatch(batchId,provider)).done,true);assert.equal(upserts.flat().length,33);assert.equal((await store.processIndexBatch(batchId,provider)).processed,0);
49:  hits=[{memoryId:records[0].id,revision:'stale',score:1},{memoryId:memory('foreign').id,revision:'foreign',score:1}];assert.deepEqual(await store.search(user.user.id,pool.id,'query',provider),[]);
50:  await store.index(user.user.id,pool.id,provider);const runKey='INDEX-RUN#'+createHash('sha256').update(provider.identity).digest('hex');const run=await db.get(`POOL#${pool.id}`,runKey);await store.index(user.user.id,pool.id,provider);assert.equal((await db.get(`POOL#${pool.id}`,runKey))?.batchId,run?.batchId);let done=false;while(!done)done=(await store.processIndexBatch(String(run?.batchId),provider)).done;assert.equal(upserts.flat().length,33,'AC5 ready revisions are not embedded again');await assert.rejects(store.index(user.user.id,pool.id,provider),/cooldown/);
51:  const correct=upserts.flat().find(r=>r.memoryId===records[0].id)!;hits=[{memoryId:correct.memoryId,revision:correct.revision,score:0.8}];assert.equal((await store.search(user.user.id,pool.id,'query',provider))[0].id,correct.memoryId);
52:  await assert.rejects(store.search(user.user.id,pool.id,'query',{identity:'test:v1',embed:async()=>{await store.revokeUser(user.user.id);return [[1,0]];}}),/Unauthorized/);
53: });
```


## src/repositories.ts

SHA-256: 27d75079804763b098a23b8843cfec6273875671e83d55034f3885ed17d4e741


### src/repositories.ts:1

```text
1: import type {TeamMemory,TeamUser,TeamPool,TeamMember,TeamShare} from './team-store.js';
2: import type {ShareInput,Snapshot,Mailer} from './executive.js';
3: import type {DeliveryStatus,InvitationMessage,SecureMailer} from './delivery.js';
4: import type {Memory,MemoryProvenance,Bundle,EmbeddingProvider,Hit} from './types.js';
5: import type {PolicyLayers} from './policy.js';
6: export type Awaitable<T> = T | Promise<T>;
7: export interface MemoryPage {memories:TeamMemory[];nextCursor?:string}
8: export interface ShareSummary {id:string;title:string;recipients:string[];expiresAt:number;revoked:boolean;count:number}
9: export interface SharePage {shares:ShareSummary[];nextCursor?:string}
10: export interface TeamRepository {
11:  readonly sourceServer:string;
12:  readonly indexingMode?:'queued';
13:  close():Awaitable<void>;
14:  createUser(name:string):Awaitable<{user:TeamUser;token:string}>;
15:  accessUser(issuer:string,subject:string,email:string):Awaitable<TeamUser>;
16:  getUser(id:string):Awaitable<TeamUser>;
17:  authenticate(token:string):Awaitable<TeamUser>;
18:  revokeUser(id:string):Awaitable<void>;
19:  createPool(actor:string,name:string,visibility:TeamPool['visibility']):Awaitable<TeamPool>;
20:  listPools(actor:string):Awaitable<TeamPool[]>;
21:  getPool(actor:string,pool:string):Awaitable<TeamPool>;
22:  grantMember(actor:string,pool:string,userId:string,role:'reader'|'writer'):Awaitable<void>;
23:  listMembers(actor:string,pool:string):Awaitable<TeamMember[]>;
24:  putMemory(actor:string,pool:string,memory:Memory):Awaitable<{id:string;created:boolean}>;
25:  putMemories(actor:string,pool:string,memories:Memory[],provenance?:MemoryProvenance[]):Awaitable<{imported:number;ids:string[]}>;
26:  listMemories(actor:string,pool:string):Awaitable<TeamMemory[]>;
27:  getMemories(actor:string,pool:string,ids:string[]):Awaitable<Memory[]>;
28:  exportBundle(actor:string,pool:string,ids:string[]):Awaitable<Bundle>;
29:  recordShare(actor:string,pool:string,shareId:string,ids:string[]):Awaitable<void>;
30:  listShares(actor:string,pool:string):Awaitable<TeamShare[]>;
31:  authorizeShareRevocation(actor:string,pool:string,shareId:string):Awaitable<void>;
32:  setPolicy(actor:string,pool:string,scope:keyof PolicyLayers,key:string,policy:unknown):Awaitable<void>;
33:  getPolicies(actor:string,pool:string,repository?:string,conversation?:string):Awaitable<PolicyLayers>;
34:  index(actor:string,pool:string,provider:EmbeddingProvider):Promise<number>;
35:  search(actor:string,pool:string,query:string,provider:EmbeddingProvider,limit?:number):Promise<Hit[]>;
36:  listSharePage?(actor:string,pool:string,options?:{limit?:number;cursor?:string}):Promise<SharePage>;
37:  rotatePersonalToken?(actor:string):Promise<{token:string}>;
38:  listMemoryPage?(actor:string,pool:string,options?:{limit?:number;cursor?:string}):Awaitable<MemoryPage>;
39:  createShare?(actor:string,pool:string,input:ShareInput & {ids:string[]}):Promise<Snapshot>;
40: }
41: export interface ShareRepository {
42:  close():Awaitable<void>;
43:  create(value:unknown):Awaitable<Snapshot>;
44:  get(id:string):Awaitable<Snapshot>;
45:  list():Awaitable<ShareSummary[]>;
46:  updateContent(id:string,value:unknown):Awaitable<Snapshot>;
47:  revoke(id:string):Awaitable<void>;
48:  invitation(id:string,email:string):Awaitable<string>;
49:  challenge(id:string,email:string,mailer:Mailer):Promise<void>;
50:  verify(id:string,email:string,code:string):Awaitable<string>;
51:  authorize(id:string,token:string):Awaitable<Snapshot>;
52: }
53: export interface DeliveryRepository {
54:  reserveCode(email:string):Awaitable<void>;
55:  send(actor:string,share:string,messages:InvitationMessage[],mailer:SecureMailer):Awaitable<DeliveryStatus[]>;
56:  status(share:string):Awaitable<DeliveryStatus[]>;
57:  statuses(shares:string[]):Awaitable<Map<string,DeliveryStatus[]>>;
58:  runBatch?(mailer:SecureMailer,limit?:number):Promise<number>;
59:  checkVerification?(action:'code'|'verify',address:string,scope:string):Promise<void>;
60: }
61: export type {DeliveryStatus,InvitationMessage};
```
