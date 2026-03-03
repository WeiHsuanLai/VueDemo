<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <!-- 導覽列按鈕 -->
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <!-- 標題 -->
        <q-toolbar-title> Quasar App </q-toolbar-title>

        <!-- 版本 -->
        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <!-- 左側導覽列 -->
    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <!-- 連結列表 -->
        <EssentialLink v-for="link in linksList" :key="link.title" v-bind="link" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import EssentialLink, { type EssentialLinkProps } from 'components/EssentialLink.vue';

const linksList: EssentialLinkProps[] = [
  {
    title: '首頁',
    caption: '回首頁',
    icon: 'home',
    link: '/',
  },
  {
    title: '設定',
    caption: '個人與系統設定',
    icon: 'settings',
    link: '/settings',
  },
  {
    title: 'Docs',
    caption: 'Quasar 官方文件',
    icon: 'school',
    link: 'https://quasar.dev',
  },
  {
    title: '網站Github',
    caption: 'github.com/WeiHsuanLai/VueDemo',
    icon: 'code',
    link: 'https://github.com/WeiHsuanLai/VueDemo',
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>
