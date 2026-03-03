<template>
  <q-page class="flex flex-center">
    <div class="column items-center text-center q-gutter-md" style="max-width: 800px">
      <div class="text-h4 text-primary text-weight-bold">目前位置與天氣</div>

      <!-- 地理位置與天氣卡片 -->
      <q-card
        flat
        bordered
        class="q-pa-lg q-mt-lg bg-white shadow-1"
        style="min-width: 350px; border-radius: 12px"
      >
        <!-- 載入中狀態 -->
        <div v-if="loadingLocation || loadingWeather" class="column items-center q-py-xl">
          <q-spinner-grid color="primary" size="3em" />
          <div class="text-subtitle1 q-mt-md text-grey-7">{{ loadingMessage }}</div>
        </div>

        <!-- 成功顯示結果 -->
        <div v-else-if="location && weather" class="column items-center">
          <!-- 天氣圖示與溫度 -->
          <div class="row items-center q-gutter-md q-mb-md">
            <q-icon :name="getWeatherIcon(weather.weatherCode)" size="4rem" color="orange-8" />
            <div class="column items-start">
              <div class="text-h3 text-weight-light">{{ Math.round(weather.temperature) }}°C</div>
              <div class="text-subtitle1 text-grey-8">
                {{ getWeatherDesc(weather.weatherCode) }}
              </div>
            </div>
          </div>

          <q-separator horizontal class="full-width q-my-md" />

          <!-- 詳細數據 -->
          <div class="row full-width justify-around q-gutter-sm">
            <div class="column items-center">
              <div class="text-caption text-grey-6">濕度</div>
              <div class="text-body1 text-weight-medium">{{ weather.humidity }}%</div>
            </div>
            <div class="column items-center">
              <div class="text-caption text-grey-6">緯度</div>
              <div class="text-body2 font-mono">{{ location.latitude.toFixed(4) }}</div>
            </div>
            <div class="column items-center">
              <div class="text-caption text-grey-6">經度</div>
              <div class="text-body2 font-mono">{{ location.longitude.toFixed(4) }}</div>
            </div>
          </div>

          <q-btn flat round color="primary" icon="refresh" @click="getLocation" class="q-mt-lg">
            <q-tooltip>更新數據</q-tooltip>
          </q-btn>
        </div>

        <!-- 錯誤狀態 -->
        <div v-else class="column items-center q-py-md">
          <q-icon name="error_outline" size="3rem" color="negative" />
          <div class="text-body1 text-negative q-mt-sm">{{ errorMessage || '無法取得數據' }}</div>
          <q-btn
            unelevated
            rounded
            color="primary"
            icon="my_location"
            label="手動重試"
            @click="getLocation"
            class="q-mt-md"
          />
        </div>
      </q-card>

      <div class="text-caption text-grey-6 q-mt-xl">數據由 Open-Meteo & 瀏覽器定位提供</div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';

// 定義型別
interface LocationCoords {
  latitude: number;
  longitude: number;
}

// Open-Meteo API 回傳的天氣資料結構
interface WeatherData {
  temperature: number;
  humidity: number;
  weatherCode: number;
}

const location = ref<LocationCoords | null>(null);
const weather = ref<WeatherData | null>(null);
const loadingLocation = ref(false);
const loadingWeather = ref(false);
const errorMessage = ref('');

const loadingMessage = computed(() => {
  if (loadingLocation.value) return '正在精確定位中...';
  if (loadingWeather.value) return '正在抓取天氣資訊...';
  return '';
});

// WMO 天氣代碼解釋與圖示對照
const getWeatherDesc = (code: number) => {
  if (code === 0) return '晴天';
  if (code >= 1 && code <= 3) return '多雲';
  if (code >= 45 && code <= 48) return '霧氣';
  if (code >= 51 && code <= 67) return '毛毛雨/下雨';
  if (code >= 71 && code <= 77) return '降雪';
  if (code >= 80 && code <= 82) return '陣雨';
  if (code >= 95) return '雷雨';
  return '未知天氣';
};

const getWeatherIcon = (code: number) => {
  if (code === 0) return 'wb_sunny';
  if (code >= 1 && code <= 3) return 'wb_cloudy';
  if (code >= 45 && code <= 48) return 'cloud_queue';
  if (code >= 51 && code <= 67) return 'umbrella';
  if (code >= 71 && code <= 77) return 'ac_unit';
  if (code >= 80 && code <= 82) return 'showers';
  if (code >= 95) return 'thunderstorm';
  return 'question_mark';
};

// 取得天氣資訊
const fetchWeather = async (lat: number, lon: number) => {
  loadingWeather.value = true;
  try {
    const response = await axios.get('https://api.open-meteo.com/v1/forecast', {
      params: {
        latitude: lat,
        longitude: lon,
        current: 'temperature_2m,relative_humidity_2m,weather_code',
      },
    });

    const current = response.data.current;
    weather.value = {
      temperature: current.temperature_2m,
      humidity: current.relative_humidity_2m,
      weatherCode: current.weather_code,
    };
  } catch (error) {
    console.error('天氣 API 錯誤:', error);
    errorMessage.value = '無法連接到天氣服務。';
  } finally {
    loadingWeather.value = false;
  }
};

// 取得位置資訊
const getLocation = () => {
  loadingLocation.value = true;
  errorMessage.value = '';
  location.value = null;
  weather.value = null;

  if (!navigator.geolocation) {
    errorMessage.value = '您的瀏覽器不支援地理位置功能。';
    loadingLocation.value = false;
    return;
  }

  // 使用高精確度定位，並設定超時
  navigator.geolocation.getCurrentPosition(
    (position) => {
      const lat = position.coords.latitude;
      const lon = position.coords.longitude;
      location.value = { latitude: lat, longitude: lon };
      loadingLocation.value = false;

      // 成功定位後，呼叫天氣 API
      void fetchWeather(lat, lon);
    },
    (error) => {
      loadingLocation.value = false;
      console.error('定位錯誤:', error);
      errorMessage.value = '定位失敗：' + (error.code === 1 ? '權限被拒絕' : '無法偵測位置');
    },
    { enableHighAccuracy: true, timeout: 10000 },
  );
};

// 組件掛載後自動取得位置與天氣
onMounted(() => {
  getLocation();
});
</script>
