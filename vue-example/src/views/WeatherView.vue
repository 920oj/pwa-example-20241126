<script setup lang="ts">
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import type { IWeatherInfo } from '@/type/weather'

const weatherInfo = ref<IWeatherInfo>()
const route = useRoute()

const getWeatherInfo = async () => {
  const id = route.params.id
  if (!id) {
    alert('IDが指定されていません')
    return
  }

  try {
    const response = await fetch(`https://weather.tsukumijima.net/api/forecast/city/${id}`)
    weatherInfo.value = await response.json()
  } catch (error) {
    alert('天気情報の取得に失敗しました')
    console.error('天気情報の取得に失敗しました:', error)
  }
}
getWeatherInfo()
</script>

<template>
  <router-link to="/" class="back-button">
    <span class="back-icon">←</span>
    戻る
  </router-link>
  <div class="weather-container">
    <h1 class="title">天気予報</h1>

    <template v-if="weatherInfo">
      <div class="current-weather">
        <div class="weather-header">
          <h2>{{ weatherInfo.title }}</h2>
          <p class="update-time">更新: {{ weatherInfo.publicTimeFormatted }}</p>
        </div>

        <div class="forecast-grid">
          <div v-for="forecast in weatherInfo.forecasts" :key="forecast.date" class="forecast-card">
            <h3>{{ forecast.dateLabel }}</h3>
            <img :src="forecast.image.url" :alt="forecast.image.title" class="weather-icon" />
            <p class="telop">{{ forecast.telop }}</p>
            <div class="temperature">
              <p v-if="forecast.temperature.max.celsius">
                最高: {{ forecast.temperature.max.celsius }}°C
              </p>
              <p v-if="forecast.temperature.min.celsius">
                最低: {{ forecast.temperature.min.celsius }}°C
              </p>
            </div>
            <div class="rain-chance">
              <p>降水確率</p>
              <div class="rain-times">
                <span>午前: {{ forecast.chanceOfRain.T06_12 }}</span>
                <span>午後: {{ forecast.chanceOfRain.T12_18 }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="weather-description">
        <h3>詳細予報</h3>
        <p>{{ weatherInfo.description.text }}</p>
      </div>
    </template>

    <div v-else class="error">
      <p>天気情報を取得できませんでした。</p>
    </div>
  </div>
</template>

<style scoped>
.back-button {
  position: fixed;
  top: 20px;
  left: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  background-color: white;
  border-radius: 25px;
  text-decoration: none;
  color: #2c3e50;
  font-weight: 500;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.back-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.back-icon {
  font-size: 1.2rem;
}
.weather-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.title {
  font-size: 2.5rem;
  color: #2c3e50;
  text-align: center;
  margin-bottom: 2rem;
}

.loading {
  text-align: center;
  padding: 2rem;
}

.spinner {
  width: 50px;
  height: 50px;
  border: 5px solid #f3f3f3;
  border-top: 5px solid #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.forecast-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.forecast-card {
  background: white;
  border-radius: 15px;
  padding: 1.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.forecast-card:hover {
  transform: translateY(-5px);
}

.weather-icon {
  width: 100px;
  height: 100px;
  margin: 1rem auto;
  display: block;
}

.telop {
  font-size: 1.25rem;
  font-weight: bold;
  text-align: center;
  color: #2c3e50;
}

.temperature {
  margin: 1rem 0;
  text-align: center;
}

.rain-chance {
  background: #f8f9fa;
  padding: 0.8rem;
  border-radius: 8px;
  margin-top: 1rem;
}

.rain-times {
  display: flex;
  justify-content: space-around;
  margin-top: 0.5rem;
}

.update-time {
  color: #666;
  text-align: center;
  font-size: 0.9rem;
}

.weather-description {
  background: white;
  border-radius: 15px;
  padding: 1.5rem;
  margin: 2rem 0;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.weather-description h3 {
  color: #2c3e50;
  margin-bottom: 1rem;
  font-size: 1.3rem;
}

.weather-description p {
  line-height: 1.6;
  color: #4a5568;
  white-space: pre-line;
}

@media (max-width: 768px) {
  .weather-container {
    padding: 1rem;
  }

  .title {
    font-size: 2rem;
  }
}
</style>
