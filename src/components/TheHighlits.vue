<script setup>
import { getPreasureMm, getTime } from "../utils";
import { computed } from "vue";
const props = defineProps({
    weatherInfo: {
        type: [Object, null],
        rquired: true,
    },
    isError: {
        type: Boolean,
        rquired: true,
    },
});
const timezone = computed(() => props.weatherInfo?.timezone);
const sunriseTime = computed(() => {
    return getTime(props.weatherInfo?.sys?.sunrise + timezone.value);
});
const sunsetTime = computed(() => {
    return getTime(props.weatherInfo?.sys?.sunset + timezone.value);
});
</script>
<template>
    <section class="highlits rounded-4 p-3" v-if="!isError">
        <div class="row">
            <div class="col mb-2">Today's Highlights</div>
        </div>
        <div class="row g-3">
            <div class="col-md-4 col-lg-4 d-flex flex-column">
                <div class="highlit d-flex flex-column flex-grow-1">
                    <div class="highlit-top d-flex flex-column flex-grow-1">
                        <p class="highlit-name">Wind</p>
                        <img
                            src="../assets/img/equalizer (2).png"
                            class="highlit-img img-fluid"
                            alt=""
                        />
                        <div
                            class="highlit-numbers d-flex justify-content-between mt-auto pb-2"
                        >
                            <span
                                ><b>{{ weatherInfo?.wind?.speed }}</b> m/s</span
                            >
                            <span
                                ><b>{{ weatherInfo?.wind?.deg }}</b> deg</span
                            >
                        </div>
                    </div>
                    <div class="highlit-bottom">
                        <p class="highlit-description-name">Wind gusts</p>
                        <span
                            v-if="weatherInfo?.wind?.gust"
                            class="highlit-description-speed"
                        >
                            <b>{{ Math.round(weatherInfo?.wind?.gust) }}</b> m/s
                        </span>
                        <p class="highlit-description-info">
                            Learn
                            <a
                                href="https://www.windy.com/articles/weather-phenomena-what-s-the-difference-between-sustained-winds-and-wind-gusts-10390?satellite,7.798,115.137,5"
                                target="_blank"
                                >more</a
                            >
                            about gusts
                        </p>
                    </div>
                </div>
            </div>
            <div class="col-md-4 col-lg-4 d-flex flex-column">
                <div class="highlit d-flex flex-column flex-grow-1">
                    <div class="highlit-top d-flex flex-column flex-grow-1">
                        <p class="highlit-name">Pressure</p>
                        <img
                            src="../assets/img/barometer.png"
                            class="highlit-img img-fluid"
                            alt=""
                        />
                        <div
                            class="highlit-numbers d-flex justify-content-center mt-auto pb-2"
                        >
                            <span
                                ><b>{{
                                    getPreasureMm(weatherInfo?.main?.pressure)
                                }}</b>
                                mm</span
                            >
                        </div>
                    </div>
                    <div class="highlit-bottom">
                        <p class="highlit-description-name">Feels like</p>
                        <span class="highlit-description-speed">
                            <b>{{
                                Math.round(weatherInfo?.main?.feels_like)
                            }}</b>
                            °C
                        </span>
                        <p class="highlit-description-info">
                            How hot or cold it really feels
                        </p>
                    </div>
                </div>
            </div>
            <div class="col-md-4 col-lg-4 d-flex flex-column">
                <div class="highlit d-flex flex-column flex-grow-1">
                    <div class="highlit-top d-flex flex-column flex-grow-1">
                        <p class="highlit-name">Cloudiness</p>
                        <img
                            src="../assets/img/sun-moving.png"
                            class="highlit-img img-fluid"
                            alt=""
                        />
                        <div class="highlit-numbers mt-auto pb-2">
                            <div class="states">
                                <div class="state">
                                    <div class="state-pic"></div>
                                    <div class="state-title">Sunrise</div>
                                    <div class="state-time">
                                        <b> {{ sunriseTime }}</b>
                                    </div>
                                </div>
                                <div class="state">
                                    <div
                                        class="state-pic state-pic--flipped"
                                    ></div>
                                    <div class="state-title">Sunset</div>
                                    <div class="state-time">
                                        <b>{{ sunsetTime }}</b>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="highlit-bottom">
                        <p class="highlit-description-name">Cloudiness</p>
                        <span class="highlit-description-speed">
                            <b>{{ weatherInfo?.clouds?.all }}</b> %
                        </span>
                        <p class="highlit-description-info">
                            The sky fraction obscured by clouds
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<style scoped lang="scss">
.highlits {
    background: url(../assets/img/gradient-4.jpg) no-repeat center/cover;
}
.highlit {
    &-top {
        padding: 0.75rem;
        min-height: 15rem;
        padding: 1rem;
        background: url(../assets/img/gradient-2.jpg) 50% 50% / cover no-repeat;
        border-radius: 0.5rem;
    }
    &-bottom {
        margin-top: 0.75rem;
        padding: 0.75rem 1rem;
        background: url(../assets/img/gradient-2.jpg) 50% 50% / cover no-repeat;
        border-radius: 0.5rem;
    }
    &-img {
        display: block;
        margin: 0 auto;
        object-fit: contain;
        height: 9rem;
    }
    &-description-info {
        font-size: 0.6rem;
    }
    .states {
        display: flex;
        justify-content: space-between;
    }
    .state-pic {
        width: 20px;
        height: 20px;
        margin-bottom: 6px;
        background: url("../assets/img/sun.svg") no-repeat 50% 50%;
        background-size: cover;
    }
    .state-title {
        // font-size: 12px;
        color: #ffd347;
    }
    .state:last-child {
        text-align: right;
    }
    .state-pic--flipped {
        margin-left: auto;
        -webkit-transform: scaleX(-1);
        transform: scaleX(-1);
    }
}
</style>
