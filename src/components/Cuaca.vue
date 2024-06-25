<template>
  <q-page-container class="no-scroll">
    <q-page class="flex flex-center">
      <div class="search-container">
        <div class="search-content">
          <q-input
            filled
            v-model="city"
            @keyup.enter="fetchWeather"
            label="Masukkan Nama Kota"
            class="search-input q-mb-md"
            dense
            color="black"
          />
          <q-btn @click="fetchWeather" label="Get Weather" class="search-btn" />
        </div>
        <div v-if="weather" class="weather-info">
          <h3>{{ weather.name }}, {{ weather.sys.country }}</h3>
          <p>Temperature: {{ weather.main.temp }}°C</p>
          <p>Weather: {{ weather.weather[0].description }}</p>
          <p>Humidity: {{ weather.main.humidity }}%</p>
          <p>Wind Speed: {{ weather.wind.speed }} m/s</p>
        </div>
      </div>
    </q-page>
  </q-page-container>
  <video id="backgroundv" loop autoplay muted :src="videoSrc"></video>
</template>

<script setup>
import { ref, computed } from 'vue';
import axios from 'axios';
import cloudsVideo from '../assets/clouds.mp4';
import rainVideo from '../assets/rain.mp4';
import windVideo from '../assets/wind.mp4';
import snowVideo from '../assets/snow.mp4';
import clearVideo from '../assets/clear.mp4';
import mistVideo from '../assets/mist.mp4';
import thunderstormVideo from '../assets/thunderstorm.mp4';

const city = ref('');
const weather = ref(null);
const videoSources = {
  clouds: cloudsVideo,
  rain: rainVideo,
  wind: windVideo,
  snow: snowVideo,
  clear: clearVideo,
  mist: mistVideo,
  thunderstorm: thunderstormVideo,
};
const defaultVideo = clearVideo;

const videoSrc = computed(() => {
  if (!weather.value) return defaultVideo;
  const description = weather.value.weather[0].description.toLowerCase();
  if (description.includes('cloud')) return videoSources.clouds;
  if (description.includes('rain')) return videoSources.rain;
  if (description.includes('wind')) return videoSources.wind;
  if (description.includes('snow')) return videoSources.snow;
  if (description.includes('clear')) return videoSources.clear;
  if (description.includes('mist')) return videoSources.mist;
  if (description.includes('thunderstorm')) return videoSources.thunderstorm;
  return defaultVideo;
});

const fetchWeather = async () => {
  const apiKey = 'f9edb91d7ad66037d883164f825fe6ac';
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&units=metric&appid=${apiKey}`;
  try {
    const response = await axios.get(url);
    weather.value = response.data;
  } catch (error) {
    console.error('Error fetching the weather data:', error);
    alert('Gagal mengambil data cuaca. Silakan coba lagi.');
  }
};
</script>

<style scoped>
#backgroundv {
  position: fixed;
  right: 0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
  z-index: -1;
}
.no-scroll {
  overflow: hidden;
}
.q-page-container {
  overflow: hidden;
}
.search-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.search-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  max-width: 600px;
  height: calc(100vh - 150px);
}
.search-input {
  width: 100%;
  margin-bottom: 20px;
  background-color: white;
}
.search-btn {
  width: 200px;
  height: 40px;
  font-size: 16px;
  font-weight: bold;
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  border: none;
  color: white;
}
.q-btn.search-btn .q-btn__content {
  text-transform: none;
}
.text-center {
  text-align: left;
}
.weather-info {
  margin-top: 20px;
  background-color: rgba(165, 143, 231, 0.5);
  padding: 20px;
  border-radius: 10%;
  backdrop-filter: blur(10px);
}
.q-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 0;
}
</style>
