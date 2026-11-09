<script setup>
defineProps({ path: { type: String, required: true } })
const base = import.meta.env.BASE_URL
</script>
<template><a :href="base + path"><slot /></a></template>
