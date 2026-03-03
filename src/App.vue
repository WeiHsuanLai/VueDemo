<template>
  <router-view />
</template>

<script setup lang="ts">
import { useQuasar } from 'quasar';
import { onBeforeMount } from 'vue';

const $q = useQuasar();

// 全域初始化：在渲染前讀取 localStorage 設定並套用
onBeforeMount(() => {
  const savedDarkMode = localStorage.getItem('darkMode');
  if (savedDarkMode !== null) {
    $q.dark.set(savedDarkMode === 'true');
  }
});
</script>
