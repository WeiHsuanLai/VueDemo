<template>
  <q-page class="column items-center">
    <!-- Hero Section -->
    <section
      id="hero"
      class="full-width q-pa-xl bg-grey-1 flex flex-center"
      style="min-height: 90vh"
    >
      <div class="text-center reveal">
        <q-avatar
          size="180px"
          class="q-mb-xl shadow-10"
          color="grey-4"
          text-color="white"
          icon="person"
        />
        <h1 class="text-h2 text-weight-bolder q-mb-md">
          Hello, I'm <span class="text-gradient">Weihsuan Lai</span>
        </h1>
        <p class="text-h5 text-grey-8 q-mb-none">
          <span ref="typedElement"></span>
        </p>
      </div>
    </section>

    <!-- About Me Section -->
    <section id="about" class="full-width q-pa-xl bg-white">
      <div class="max-width-container q-mx-auto reveal">
        <div class="row q-col-gutter-xl items-center">
          <div class="col-12 col-md-5 text-center">
            <q-img
              src="https://cdn.quasar.dev/img/material.png"
              style="max-width: 400px; border-radius: 20px"
              class="shadow-2"
            />
          </div>
          <div class="col-12 col-md-7">
            <h2 class="text-h4 text-weight-bold q-mb-lg">About Me</h2>
            <div class="text-body1 text-grey-8 line-height-relaxed">
              <p class="q-mb-md">
                您好！我是 <strong>賴偉璿</strong>，目前任職於
                <strong>承翊系統整合股份有限公司</strong>。作為一名專注於 <strong>Vue 3</strong> 與
                <strong>TypeScript</strong>
                生態系的前端工程師，我熱衷於將複雜的業務邏輯轉化為直覺且優雅的使用者介面。
              </p>
              <p class="q-mb-md">
                我具備高度的<strong>結構化思維</strong>與對<strong>技術細節</strong>的極致追求，擅長以工程化的視角平衡視覺美感與系統效能。在開發過程中，我致力於實踐「代碼即藝術」的精髓，撰寫具備高擴展性且易於維護的乾淨程式碼 (Clean Code)，並確保每一個功能模組都能達到最優的使用者體驗。
              </p>
              <p class="q-mb-md">
                我具備深厚的<strong>企業級後台架構</strong>開發經驗，擅長處理權限控管
                (RBAC)、數據圖表整合及複雜的業務流程優化。同時，我也具備
                <strong>uniapp</strong> 跨平台開發與維護經驗，負責公司現有 APP 在 iOS 與 Android
                平台上的功能迭代與穩定性優化，為企業提供高效、統一的多端解決方案。
              </p>
              <p class="q-mb-md">
                除了技術層面，我具備<strong>健談且善於溝通</strong>的特質，能有效跨部門協調需求，並以清晰的邏輯縮短開發與業務間的認知落差。我<strong>熱愛學習新事物</strong>，對於快速迭代的技術環境保持高度熱忱，並<strong>極其重視團隊合作</strong>，相信良好的同儕互動是打造卓越產品的核心基石。
              </p>
              <p>
                目前，我正積極精進 <strong>AWS 雲端架構</strong> 與前端效能最佳化技術。同時，我也擅長運用 <strong>AI 工具輔助開發</strong>，透過精準的 Prompt Engineering 提升開發效率、優化程式碼邏輯並快速導入新技術，期許能透過技術的深度與廣度，為專案創造卓越的用戶價值。
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="full-width q-pa-xl" style="max-width: 1000px">
      <div class="reveal">
        <h2 class="text-h4 text-weight-bold q-mb-xl text-center">Work Experience</h2>
        <q-timeline color="grey-8" :layout="timelineLayout">
          <q-timeline-entry
            title="前端工程師"
            subtitle="2024/11 - 至今 | 承翊系統整合股份有限公司"
            side="right"
            icon="computer"
          >
            <div>
              主導企業級 Web 應用的前端架構開發，使用 <strong>Vue 3</strong> 與
              <strong>TypeScript</strong> 建立高效能且可維護的代碼庫。
              負責將複雜的業務需求轉化為流暢的 UI/UX，並利用
              <strong>Quasar Framework</strong> 實現跨平台兼容性。 同時，<strong
                >善於運用 AI 工具輔助開發</strong
              >，顯著提升了代碼編寫速度與單元測試覆蓋率，並優化了整體的開發工作流程。
            </div>
          </q-timeline-entry>

          <q-timeline-entry
            title="後台管理系統開發 (Enterprise Admin Panel)"
            subtitle="專案實作"
            side="left"
            icon="settings"
          >
            <div>
              開發高複雜度的後台管理介面，實現<strong>動態權限控管 (RBAC)</strong
              >、大數據量列表優化及可視化圖表 (Echarts/Chart.js) 整合。
              優化後台操作流程，提升管理端作業效率達 30% 以上。
            </div>
          </q-timeline-entry>

          <q-timeline-entry
            title="跨平台 App 維護與優化 (uniapp / Vue)"
            subtitle="現有 App 迭代"
            side="right"
            icon="smartphone"
          >
            <div>
              負責 <strong>uniapp</strong> 跨平台 App 的日常維護與功能開發，確保
              <strong>iOS 與 Android 平台</strong> 的穩定運行與介面優化，並處理跨端相容性問題。
            </div>
          </q-timeline-entry>

          <q-timeline-entry
            title="前端網頁工程師培訓學員"
            subtitle="2024/03 - 2024/08"
            side="left"
            icon="school"
          >
            <div>
              在泰山職訓局參與高強度前端工程開發訓練，在短時間內掌握
              <strong>Vue 生態系</strong> 與前端工程化思維。 期間獨立完成多項專案開發，從 UI
              排版、資料串接到部署，建立了紮實的技術開發邏輯。
            </div>
          </q-timeline-entry>

          <q-timeline-entry title="室內設計師助理" subtitle="2019 - 2021" side="right" icon="palette">
            <div>
              協助設計師進行空間規劃、CAD 施工圖繪製及現場工程進度跟進。
              透過嚴謹的製圖訓練，建立了對細節的敏銳度與對美感的堅持，並學習如何與業主及工班進行有效的跨部門溝通。
            </div>
          </q-timeline-entry>
        </q-timeline>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="full-width q-pa-xl bg-grey-2">
      <div class="text-center reveal" style="max-width: 1000px; margin: 0 auto">
        <h2 class="text-h4 text-weight-bold q-mb-xl">Expertise</h2>
        <div class="row q-col-gutter-lg">
          <div v-for="skillGroup in skillGroups" :key="skillGroup.title" class="col-12 col-sm-6">
            <q-card flat bordered class="full-height">
              <q-card-section>
                <div class="text-h6 q-mb-md text-grey-9">{{ skillGroup.title }}</div>
                <div class="flex flex-center q-gutter-sm">
                  <q-chip
                    v-for="skill in skillGroup.list"
                    :key="skill.name"
                    color="white"
                    text-color="grey-9"
                    class="text-weight-bold shadow-1"
                    size="18px"
                  >
                    <q-avatar>
                      <img :src="skill.icon" :alt="skill.name" />
                    </q-avatar>
                    {{ skill.name }}
                  </q-chip>
                </div>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Portfolio Section -->
    <section id="portfolio" class="full-width q-pa-xl" style="max-width: 1200px">
      <div class="reveal">
        <h2 class="text-h4 text-weight-bold q-mb-xl text-center">Projects</h2>
        <div class="row q-col-gutter-lg">
          <div v-for="i in 3" :key="i" class="col-12 col-sm-4">
            <q-card class="my-card cursor-pointer" flat bordered>
              <q-img src="https://cdn.quasar.dev/img/parallax2.jpg" :ratio="16 / 9" />
              <q-card-section>
                <div class="text-h6">專案名稱 {{ i }}</div>
                <div class="text-subtitle2 text-grey-7 q-mb-sm">Vue 3 + TypeScript</div>
                <div class="text-body2">
                  這是一個使用 Quasar Framework 開發的範例專案，展示了極致的 UI/UX 與效能優化。
                </div>
              </q-card-section>
              <q-card-actions align="right">
                <q-btn flat color="grey-9" label="查看更多" />
              </q-card-actions>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="full-width q-pa-xl bg-grey-10 text-white" style="min-height: 40vh; display: flex; align-items: center;">
      <div class="text-center" style="max-width: 600px; margin: 0 auto">
        <h2 class="text-h4 text-weight-bold q-mb-lg">Contact</h2>
        <div class="q-mb-xl">
          <q-btn
            flat
            no-caps
            icon="email"
            size="xl"
            :label="myEmail"
            class="text-weight-bold"
            @click="openMail"
          />
        </div>
      </div>
    </section>
  </q-page>
</template>

<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue';
import { useQuasar } from 'quasar';
import Typed from 'typed.js';

const $q = useQuasar();
const typedElement = ref<HTMLElement | null>(null);
let typed: Typed | null = null;

onMounted(() => {
  if (typedElement.value) {
    typed = new Typed(typedElement.value, {
      strings: ['Frontend Engineer | Vue 3 & TypeScript', '前端工程師 | Vue 3 & TypeScript'],
      typeSpeed: 60,
      backSpeed: 40,
      backDelay: 2000,
      loop: true,
      cursorChar: '|',
    });
  }

  // Scroll Reveal Observer
  const revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('active');
        }
      });
    },
    { threshold: 0.15 }
  );

  document.querySelectorAll('.reveal').forEach((el) => {
    revealObserver.observe(el);
  });
});

onUnmounted(() => {
  if (typed) {
    typed.destroy();
  }
});

const myEmail = 'hsuan29684@gmail.com';

const openMail = () => {
  window.location.href = `mailto:${myEmail}`;
};

interface Skill {
  name: string;
  icon: string;
}

interface SkillGroup {
  title: string;
  list: Skill[];
}

const skillGroups: SkillGroup[] = [
  {
    title: '程式語言與核心技術',
    list: [
      {
        name: 'JavaScript',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg',
      },
      {
        name: 'TypeScript',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg',
      },
      {
        name: 'HTML5',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg',
      },
      {
        name: 'CSS3',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg',
      },
    ],
  },
  {
    title: '前端框架與庫',
    list: [
      {
        name: 'Vue.js',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg',
      },
      {
        name: 'Quasar',
        icon: 'https://cdn.quasar.dev/logo-v2/svg/logo.svg',
      },
      {
        name: 'Vuetify',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuetify/vuetify-original.svg',
      },
    ],
  },
  {
    title: '後端與資料庫',
    list: [
      {
        name: 'Node.js',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg',
      },
      {
        name: 'MongoDB',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg',
      },
      {
        name: 'Express.js',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/express/express-original.svg',
      },
    ],
  },
  {
    title: '開發工具與版本控制',
    list: [
      {
        name: 'GitHub',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg',
      },
      {
        name: 'Git',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg',
      },
      {
        name: 'VS Code',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg',
      },
      {
        name: 'Vite',
        icon: 'https://upload.wikimedia.org/wikipedia/commons/f/f1/Vitejs-logo.svg',
      },
    ],
  },
  {
    title: '設計工具 (Adobe 系列)',
    list: [
      {
        name: 'Photoshop',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/photoshop/photoshop-original.svg',
      },
      {
        name: 'Illustrator',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/illustrator/illustrator-plain.svg',
      },
    ],
  },
];

const timelineLayout = computed(() => {
  return $q.screen.lt.md ? 'dense' : 'loose';
});
</script>

<style lang="scss" scoped>
section {
  padding-top: 100px;
  padding-bottom: 100px;
}

.my-card {
  transition: transform 0.3s;
  &:hover {
    transform: translateY(-10px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  }
}

.text-gradient {
  background: linear-gradient(135deg, #1976d2 0%, #9c27b0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: inline-block;
}

.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: all 1s ease-out;
}

.reveal.active {
  opacity: 1;
  transform: translateY(0);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Typed.js 游標顏色 */
:deep(.typed-cursor) {
  color: var(--q-primary);
}

/* 時間軸文字統一靠左對齊 */
:deep(.q-timeline__entry--left) {
  .q-timeline__content,
  .q-timeline__subtitle,
  .q-timeline__title {
    text-align: left !important;
  }
}
</style>
