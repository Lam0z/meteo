<script setup>
import { ref, onMounted, computed } from "vue";
import { API_KEY, BASE_URL } from "./constants";

import TheLayout from "@/components/TheLayout.vue";
import TheSity from "@/components/TheSity.vue";
import TheHighlits from "@/components/TheHighlits.vue";
import TheDescription from "@/components/TheDescription.vue";

const isError = computed(() => weatherInfo.value?.cod !== 200);

const city = ref("Kanberra");
const weatherInfo = ref(null);

const inputValue = (value) => {
    city.value = value;
    getWeather(value);
};

function getWeather() {
    fetch(`${BASE_URL}?q=${city.value}&units=metric&appid=${API_KEY}`)
        .then((response) => response.json())
        .then((data) => {
            weatherInfo.value = data;
        });
}

onMounted(getWeather);
</script>

<template>
    <TheLayout :isError="isError" :weatherInfo="weatherInfo">
        <template #default>
            <TheSity
                class=""
                :city="city"
                :weatherInfo="weatherInfo"
                @onInput="inputValue"
                :isError="isError"
            />
            <TheHighlits
                class=""
                :weatherInfo="weatherInfo"
                :isError="isError"
            />
        </template>
        <template #description>
            <TheDescription
                class=""
                v-if="weatherInfo?.weather"
                :cord="weatherInfo?.coord"
                :humidity="weatherInfo?.main.humidity"
            />
        </template>
    </TheLayout>
</template>

<style></style>
