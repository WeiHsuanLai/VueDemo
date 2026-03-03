<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">設定頁面</div>
    <p>這是新建立的設定分頁內容。</p>

    <q-card flat bordered class="q-pa-md" style="max-width: 400px">
      <q-item tag="label" v-ripple>
        <q-item-section avatar>
          <q-toggle v-model="darkMode" color="dark" />
        </q-item-section>
        <q-item-section>
          <q-item-label>深色模式</q-item-label>
        </q-item-section>
      </q-item>
    </q-card>
  </q-page>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { useQuasar } from 'quasar';

const $q = useQuasar();
const darkMode = ref($q.dark.isActive);

// 當深色模式切換時更新 Quasar 設定
watch(darkMode, (val) => {
  $q.dark.set(val);
});
</script>
