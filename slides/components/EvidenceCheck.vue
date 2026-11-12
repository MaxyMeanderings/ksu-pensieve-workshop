<script setup>
import { ref } from 'vue'
const revealed = ref(false)
</script>
<template><div class="evidence-check"><div class="cards"><div><small>RESULT</small><strong>8 / 8 passed</strong><p>The grader says the agent works.</p></div><div><small>RESPONSE EXCERPT · CASE 7</small><p>“Zoom, Discord, Stripe, or Devpost already do…”</p><p>No source URLs accompanied these alternative claims.</p></div></div><button @click="revealed = !revealed">{{ revealed ? 'Hide discussion prompt' : 'What should we inspect?' }}</button><p v-if="revealed" class="answer">The brief requires source URLs for competitor claims. Inspect every applicable requirement—even when the test is about MVP scope.</p></div></template>
<style scoped>.cards{display:grid;grid-template-columns:1fr 1.4fr;gap:22px}.cards>div{padding:22px;background:#e1e8de;border-radius:8px}.cards strong{display:block;font-size:39px;color:#0e7461;margin:12px 0}.cards small{letter-spacing:2px;color:#436158}.cards p{font-size:22px!important}button{margin-top:18px;background:#0e7461;color:white;padding:11px 18px;border:0;border-radius:5px;font-size:18px;cursor:pointer}.answer{font-size:20px!important;margin-top:14px;color:#6c4d18}</style>
