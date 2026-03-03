<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">設定頁面</div>
    <p>這是新建立的設定分頁內容。</p>

    <q-card flat bordered class="q-pa-md" style="max-width: 400px">
      <q-item tag="label" v-ripple>
        <q-item-section avatar>
          <q-toggle
            v-model="darkMode"
            color="primary"
            keep-color
            checked-icon="dark_mode"
            unchecked-icon="light_mode"
            size="lg"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label class="text-weight-bold">介面外觀</q-item-label>
          <q-item-label caption>
            目前已開啟 {{ darkMode ? '深色' : '淺色' }} 模式
          </q-item-label>
        </q-item-section>
      </q-item>
    </q-card>
  </q-page>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { useQuasar } from 'quasar';

const $q = useQuasar();

// 優先從 localStorage 讀取，若無則跟隨系統或預設值
const savedDarkMode = localStorage.getItem('darkMode');
const darkMode = ref(savedDarkMode !== null ? savedDarkMode === 'true' : $q.dark.isActive);

// 初始化時立即套用
$q.dark.set(darkMode.value);

// 當深色模式切換時更新 Quasar 設定並存入 localStorage
watch(darkMode, (val) => {
  $q.dark.set(val);
  localStorage.setItem('darkMode', val.toString());
});
</script>
