<script setup>


const {weather} = defineProps({
    weather:{
        type:Object
    }
})

</script>

<template>

    <div class="bg-white w-100 h-110 mt-20 opacity-60 rounded-2xl p-10 font-semibold text-center flex items-center flex-col gap-2">

        <p><i class="fa fa-location-arrow" aria-hidden="true"></i> {{weather.name}},{{weather.region}},{{weather.country}}</p>
        <img :src="weather.image" width="100" height="100"/>
        <p class="mt-4 text-4xl">{{ weather.temperature }} °C</p>
        <p class="text-xl">{{ weather.currentWeather }}</p>
       <div class="flex gap-2 w-full mt-5">
        <div class="w-1/2 flex flex-col border border-gray-200 rounded-md p-5 "><span>Wind : {{ weather.wind_kph  }} kph</span> <span>Gust : {{ weather.gust_kph }} kph</span></div>
        <div class="w-1/2 flex flex-col border border-gray-200 rounded-md p-5 "><span>Humidity : {{ weather.humidity }}</span> <span>Pressure: {{ weather.pressure }}</span></div>
       </div>
    </div>

</template>