<template>
  <q-item
    clickable
    v-bind="linkProps"
    exact
  >
    <q-item-section
      v-if="icon"
      avatar
    >
      <q-icon :name="icon" />
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ title }}</q-item-label>
      <q-item-label caption>{{ caption }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script setup lang="ts">
import { computed } from 'vue';

export interface EssentialLinkProps {
  title: string;
  caption?: string;
  link?: string;
  icon?: string;
  external?: boolean; // 新增：是否強制為外部連結
};

const props = withDefaults(defineProps<EssentialLinkProps>(), {
  caption: '',
  link: '#',
  icon: '',
  external: false,
});

// 自動判斷屬性
const linkProps = computed(() => {
  const isExternal = props.external || props.link.startsWith('http') || props.link.startsWith('//');
  
  if (isExternal) {
    return {
      tag: 'a',
      href: props.link,
      target: '_blank', // 外部連結通常才開新分頁
    };
  }
  
  return {
    to: props.link, // 內部路由使用 to 屬性
  };
});
</script>
