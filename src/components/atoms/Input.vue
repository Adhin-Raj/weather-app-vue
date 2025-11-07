<script setup>
import { ref } from 'vue';

const { city } = defineProps({
    city: {
        type: String
    }
})

let inputValue = ref(city)

const emit = defineEmits(['update'])

function handleSubmit() {
    const update = inputValue.value
    emit('update', update)
}

function handleInput(e) {
    const { value } = e.target
    inputValue.value = value.trim()
}

</script>


<template>
    <form @submit.prevent="handleSubmit" class="relative right-10">
        <label for="cityName" class="text-xl font-semibold mr-2 text-green-100">Enter the city:</label>
        <input class="px-2 py-2 border-3 text-gray-300 rounded-md border-blue-300 " type="text" name="cityName"
            :value="city" @input="handleInput">
        <button class="w-11 h-11 border ml-2 rounded-md cursor-pointer bg-amber-50 hover:bg-amber-300"><i
                class="fa fa-search" aria-hidden="true"></i></button>
    </form>
</template>