<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-grey-10 text-grey-4">
      <q-toolbar class="justify-center q-py-sm">
        <!-- 桌面版置中選單 -->
        <div class="gt-xs row q-gutter-x-lg">
          <div
            v-for="item in menuItems"
            :key="item.id"
            class="nav-item cursor-pointer text-weight-bold"
            :class="{ 'active-link': activeSection === item.id }"
            @click="scrollToSection(item.id)"
          >
            {{ item.label }}
          </div>
        </div>

        <!-- 行動版選單按鈕 -->
        <q-btn flat dense round icon="menu" aria-label="Menu" class="lt-sm absolute-right q-mr-md text-white" @click="toggleLeftDrawer" />
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" bordered class="lt-sm bg-grey-10 text-grey-4">
      <q-list>
        <q-item-label header class="text-grey-6">Navigation</q-item-label>
        <q-item
          v-for="item in menuItems"
          :key="item.id"
          clickable
          v-ripple
          @click="scrollToSection(item.id); leftDrawerOpen = false"
          :class="{ 'active-link': activeSection === item.id }"
        >
          <q-item-section avatar>
            <q-icon :name="item.icon" :color="activeSection === item.id ? 'white' : 'grey-4'" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ item.label }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="bg-grey-9 text-white q-pa-md text-center">
      <div>© {{ new Date().getFullYear() }} 賴偉璿. Powered by Quasar.</div>
    </q-footer>
  </q-layout>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const leftDrawerOpen = ref(false);
const activeSection = ref('hero');

const menuItems = [
  { label: 'Home', id: 'hero', icon: 'home' },
  { label: 'About', id: 'about', icon: 'person' },
  { label: 'Experience', id: 'experience', icon: 'work' },
  { label: 'Skills', id: 'skills', icon: 'star' },
  { label: 'Projects', id: 'portfolio', icon: 'code' },
  { label: 'Contact', id: 'contact', icon: 'email' }
];

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

// 改良後的 Ease-Out 捲動函式
const scrollToSection = (id: string) => {
  const el = document.getElementById(id);
  if (!el) return;

  const headerHeight = 60;
  const targetPosition = el.getBoundingClientRect().top + window.pageYOffset - headerHeight;
  const startPosition = window.pageYOffset;
  const distance = targetPosition - startPosition;
  const duration = 800;
  let startTime: number | null = null;

  const easeOutCubic = (t: number) => (--t) * t * t + 1;

  const animation = (currentTime: number) => {
    if (startTime === null) startTime = currentTime;
    const timeElapsed = currentTime - startTime;
    const progress = Math.min(timeElapsed / duration, 1);
    window.scrollTo(0, startPosition + distance * easeOutCubic(progress));
    if (timeElapsed < duration) requestAnimationFrame(animation);
  };

  requestAnimationFrame(animation);
};

// 捲動追蹤邏輯 (Scroll Spy)
let observer: IntersectionObserver | null = null;

const handleScroll = () => {
  // 檢查是否捲動到頁面底部
  const scrollPosition = window.innerHeight + window.pageYOffset;
  const pageHeight = document.documentElement.scrollHeight;
  
  // 距離底部小於 50px 時，強制選中最後一個項目
  if (scrollPosition >= pageHeight - 50) {
    const lastItem = menuItems[menuItems.length - 1];
    if (lastItem) {
      activeSection.value = lastItem.id;
    }
  }
};

onMounted(() => {
  const options = {
    root: null,
    rootMargin: '-20% 0px -70% 0px', // 向上偏移偵測範圍
    threshold: 0
  };

  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        activeSection.value = entry.target.id;
      }
    });
  }, options);

  menuItems.forEach((item) => {
    const el = document.getElementById(item.id);
    if (el) observer?.observe(el);
  });

  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  if (observer) observer.disconnect();
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style lang="scss" scoped>
.nav-item {
  transition: all 0.3s ease;
  padding: 8px 4px;
  position: relative;
  font-size: 1.1rem;
  color: #bdbdbd; // 灰白色 (grey-4)

  &:hover {
    color: #ffffff; // 懸停時為純白色
  }

  &::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 0;
    height: 2px;
    background-color: #ffffff;
    transition: all 0.3s ease;
    transform: translateX(-50%);
  }

  &:hover::after {
    width: 80%;
  }
}

.active-link {
  color: #ffffff !important; // 選中狀態為純白色
  &::after {
    width: 80% !important;
  }
}
</style>
