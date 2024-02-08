<script setup>
import { capitalizeFirstLetter } from "@/utils/index.js";
// import drizzle from "@/assets/img/weather-main/drizzle.png";
const emits = defineEmits(["onInput"]);
const props = defineProps({
    city: {
        type: String,
        rquired: true,
    },
    weatherInfo: {
        type: [Object, null],
        rquired: true,
    },

    isError: {
        type: Boolean,
        rquired: true,
    },
});

const onInput = (e) => {
    emits("onInput", e.target.value);
};
const today = new Date().toLocaleString("en-En", {
    weekday: "short",
    year: "numeric",
    month: "long",
    day: "numeric",
});
</script>
<template>
    <section class="sity rounded-4 p-3 shadow">
        <div class="sity-input-wrapper">
            <label for="forecast-input"><i class="bi bi-search"></i></label>

            <input
                id="forecast-input"
                type="text"
                class="form-control"
                placeholder="Название города + Enter"
                aria-label="Название города"
                :value="city"
                @keyup.enter="onInput"
            />
        </div>

        <div class="summary-info" v-if="!isError">
            <div class="summary mt-2">
                <img
                    :src="`./weather-main/${weatherInfo?.weather[0].description}.png`"
                    class="weather-icon"
                    alt=""
                />
            </div>
            <div class="weather">
                <div class="temp h2">
                    {{ Math.round(weatherInfo?.main.temp) }} °C
                </div>

                <div class="weather-desc text-block">
                    {{
                        capitalizeFirstLetter(
                            weatherInfo?.weather[0].description
                        )
                    }}
                </div>
            </div>
            <div class="city text-block">
                {{ weatherInfo?.name }}, {{ weatherInfo?.sys.country }}
            </div>
            <div class="date text-block">{{ today }}</div>
        </div>
    </section>
</template>
<style scoped lang="scss">
.sity {
    background: url(../assets/img/gradient-1.jpg) no-repeat center/cover;
    &-input-wrapper {
        position: relative;
    }
    input {
        border: none;
        padding-right: 2rem;
        outline: 1px solid white;
        &:focus {
            outline: none;
        }
    }
    label {
        position: absolute;
        right: 0.75rem;
        top: 50%;
        transform: translateY(-50%);
        // background: #000;
    }
    .weather-icon {
        width: 4rem;
        height: 4rem;
        background-size: contain;
        // background-image: url("../assets/img/weather-main/snow.png");
        margin: 1.25rem 0px 0.75rem;
        background-repeat: no-repeat;
        background-position: 50% 50%;
    }
    .weather {
        margin: 0rem 0rem 1.25rem;
        padding: 1.25rem 0rem;
        border-bottom: 1px solid rgba(255, 255, 255, 0.4);
    }
    .text-block {
        padding-left: 24px;
        position: relative;
        &::before {
            content: "";
            position: absolute;
            top: 50%;
            left: 0px;
            transform: translateY(-50%);
            width: 1.25rem;
            height: 1.25rem;
            margin-right: 0.4rem;
            background-size: contain;
            background-repeat: no-repeat;
            background-position: 50% 50%;
        }
    }
    .weather-desc::before {
        background-image: url(../assets/img/weather.svg);
    }
    .city {
        position: relative;
        &::before {
            background-image: url("../assets/img/location.svg");
        }
    }
    .date {
        position: relative;
        &::before {
            left: 2px;
            width: 1rem;
            height: 1rem;
            background-image: url("../assets/img/calendar.svg");
        }
    }
    .error {
        &-title {
        }
        &-message {
        }
    }
}
</style>
