<script setup>
import { computed } from 'vue'
import { useNav } from '@slidev/client'
const nav = useNav()
const sections = [
  { label: 'Set up', start: 1 },
  { label: 'The problem', start: 7 },
  { label: 'Observe + orient', start: 9 },
  { label: 'Decide', start: 14 },
  { label: 'Act + inspect', start: 19 },
  { label: 'Trust + works cited', start: 33 },
  { label: 'Challenge + repair', start: 40 },
  { label: 'Remember', start: 63 },
]
const active = computed(() => sections.reduce((found, s, i) => nav.currentPage.value >= s.start ? i : found, 0))
</script>
<template>
  <nav class="module-nav" aria-label="Presentation sections">
    <img class="ksu-nav" src="/assets/ksu-monogram.png" alt="Kennesaw State University" /><div class="nav-caption">THE WORKING LOOP</div>
    <button v-for="(section, i) in sections" :key="section.start"
      :class="{ past: i < active, current: i === active }"
      :aria-current="i === active ? 'step' : undefined" @click="nav.go(section.start)">
      <span aria-hidden="true">{{ i < active ? '✓' : i === active ? '●' : '○' }}</span>
      {{ section.label }}
    </button>
  </nav>
</template>
<style>
.module-nav{position:absolute;left:24px;top:180px;width:156px;z-index:30;font-family:'Source Code Pro',monospace}
.nav-caption{font-size:10px;letter-spacing:1.5px;color:#d8ccbc;margin-bottom:20px}
.module-nav button{display:flex;gap:9px;align-items:center;text-align:left;width:100%;border:0;border-left:2px solid transparent;background:transparent;color:#aaa69e;padding:13px 6px;font:inherit;font-size:12px;line-height:1.5;cursor:pointer}
.module-nav button.current{color:#f6d18d;background:#30291d;border-left-color:#e5b65e}
.module-nav button.past{color:#c8c4b8}
.module-nav button:hover,.module-nav button:focus-visible{color:#fff;outline:1px solid #e5b65e}
</style>
