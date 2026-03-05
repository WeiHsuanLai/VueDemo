<template>
  <q-page class="column items-center">
    <!-- Hero / About Section -->
    <section
      id="about"
      class="full-width q-pa-xl bg-grey-1 flex flex-center"
      style="min-height: 90vh"
    >
      <div class="text-center animate-fade">
        <q-avatar
          size="180px"
          class="q-mb-xl shadow-10"
          color="grey-4"
          text-color="white"
          icon="person"
        />
        <h1 class="text-h2 text-weight-bolder q-mb-md">
          <span ref="typedElement"></span>
        </h1>
        <p class="text-h5 text-grey-8 q-mb-none">Frontend Engineer | Vue 3 & TypeScript</p>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="full-width q-pa-xl" style="max-width: 1000px">
      <h2 class="text-h4 text-weight-bold q-mb-xl text-center">
        <q-icon name="work" color="grey-8" class="q-mr-sm" />Work Experience
      </h2>
      <q-timeline color="grey-8" :layout="timelineLayout">
        <q-timeline-entry title="前端工程師" subtitle="2022 - 至今" side="right" icon="computer">
          <div>
            主導企業級 Web 應用的前端架構開發，使用 <strong>Vue 3</strong> 與
            <strong>TypeScript</strong> 建立高效能且可維護的代碼庫。
            負責將複雜的業務需求轉化為流暢的 UI/UX，並利用
            <strong>Quasar Framework</strong> 實現跨平台兼容性。
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
    </section>

    <!-- Skills Section -->
    <section id="skills" class="full-width q-pa-xl bg-grey-2">
      <div class="text-center" style="max-width: 1000px; margin: 0 auto">
        <h2 class="text-h4 text-weight-bold q-mb-xl">專業技能</h2>
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
      <h2 class="text-h4 text-weight-bold q-mb-xl text-center">
        <q-icon name="code" color="grey-8" class="q-mr-sm" />精選作品
      </h2>
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
    </section>

    <!-- Contact Section -->
    <section id="contact" class="full-width q-pa-xl bg-grey-10 text-white">
      <div class="text-center" style="max-width: 600px; margin: 0 auto">
        <h2 class="text-h4 text-weight-bold q-mb-lg">與我聯絡</h2>
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
      strings: ["Hello, I'm Weihsuan Lai", '你好，我是賴偉璿'],
      typeSpeed: 60,
      backSpeed: 40,
      backDelay: 2000,
      loop: true,
      cursorChar: '|',
    });
  }
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
    title: '前端開發',
    list: [
      {
        name: 'Vue 3',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg',
      },
      {
        name: 'TypeScript',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg',
      },
      {
        name: 'Quasar',
        icon: 'https://cdn.quasar.dev/logo-v2/svg/logo.svg',
      },
      {
        name: 'Vite',
        icon: 'https://upload.wikimedia.org/wikipedia/commons/f/f1/Vitejs-logo.svg',
      },
      {
        name: 'Pinia',
        icon: 'https://pinia.vuejs.org/logo.svg',
      },
      {
        name: 'Tailwind CSS',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg',
      },
    ],
  },
  {
    title: '後端與工具',
    list: [
      {
        name: 'Node.js',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg',
      },
      {
        name: 'Express',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/express/express-original.svg',
      },
      {
        name: 'PostgreSQL',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg',
      },
      {
        name: 'AWS',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/amazonwebservices/amazonwebservices-original-wordmark.svg',
      },
      {
        name: 'Docker',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg',
      },
      {
        name: 'Git',
        icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg',
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

.animate-fade {
  animation: fadeIn 1.5s ease-in;
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
</style>
