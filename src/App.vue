<script setup>
import { ref } from 'vue';
import Input from './components/atoms/Input.vue';

const city = ref('Kerala')

const update = (data) => {
  city.value = data
  fetchWeather()
}

const apiKey = import.meta.env.VITE_WEATHER_API

const fetchWeather = async () => {
  try {
    const response = await fetch(`http://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city.value}`)
    const data = await response.json()
    console.log(data.current.temp_c)
  } catch (error) {
    console.log("Error", error)
  }
}

fetchWeather()

</script>

<template>
  <main class="flex flex-col pt-5 items-center h-dvh w-dvw bg-center"
    style="background-image: url('/background-image.jpg')">
    <h1 class="my-5 text-purple-400 text-4xl font-bold text-center">Weather App</h1>
    <Input @update="update" :city="city" />

  </main>
</template>

<style scoped></style>
