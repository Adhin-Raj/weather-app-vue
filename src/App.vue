<script setup>
import { ref } from 'vue';
import Input from './components/atoms/Input.vue';
import DisplayWeather from './components/atoms/DisplayWeather.vue';
import { useToast } from 'vue-toastification';


let state = ref({
  isLoading: false
})
const toast = useToast();

const city = ref('Kochi')
const weatherData = ref({
  temperature: "",
  name: "",
  region: "",
  country: "",
  wind_kph: "",
  pressure: "",
  humidity: "",
  gust_kph: "",
  image: "",
  currentWeather: ""
})

const update = (data) => {
  city.value = data
  fetchWeather()
}

const apiKey = import.meta.env.VITE_WEATHER_API

const fetchWeather = async () => {
  try {
    state.value.isLoading = true
    const response = await fetch(`http://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city.value}`)
    const data = await response.json()
    console.log(data)
    weatherData.value = {
      temperature: data.current.temp_c,
      name: data.location.name, region: data.location.region,
      country: data.location.country, wind_kph: data.current.wind_kph,
      pressure: data.current.pressure_in, humidity: data.current.humidity,
      gust_kph: data.current.gust_kph, image: data.current.condition.icon,
      currentWeather: data.current.condition.text
    }
    toast.success("Weather Data fetched successfully...!")
  } catch (error) {
    console.log("Error", error)
    toast.error("Error in fetching data...!")
  }
  finally {
    state.value.isLoading = false
  }
}


fetchWeather()

</script>

<template>
  <main class="flex flex-col pt-5 items-center h-dvh w-dvw bg-center"
    style="background-image: url('/background-image.jpg')">
    <h1 class="my-5 text-purple-400 text-4xl font-bold text-center">Weather App</h1>
    <Input @update="update" :city="city" />
    <div v-show="state.isLoading" class="text-6xl text-blue-500 animate-spin">
      <i class="fa-solid fa-spinner" aria-hidden="true"></i>
    </div>
    <DisplayWeather :weather="weatherData" />
  </main>
</template>

<style scoped></style>
