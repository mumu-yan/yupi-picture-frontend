<script setup lang="ts">
import BasicLayout from '@/layouts/BasicLayout.vue'
import { useLoginUserStore } from '@/stores/useLoginUserStore.ts'

const loginUserStore = useLoginUserStore()
loginUserStore.fetchLoginUser()
</script>

<template>
  <div id="app">
    <basic-layout />
  </div>
</template>

<style scoped></style>
