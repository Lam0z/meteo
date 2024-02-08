<script setup>
import { capitalizeFirstLetter } from "../utils";
const props = defineProps({
    isError: {
        type: Boolean,
        rquired: true,
    },
    weatherInfo: {
        type: [Object, null],
        rquired: true,
    },
});
// console.log(props.weatherInfo?);
</script>
<template>
    <main class="wrapper d-flex">
        <div
            class="wrapper-container d-flex justify-content-center align-items-center flex-grow-1 m-3"
        >
            <div class="container">
                <div
                    class="main-content"
                    :class="{ 'main-content__error': isError }"
                >
                    <div
                        class="error mt-2 text-center font-monospace"
                        v-if="weatherInfo?.message"
                    >
                        <div class="error-title text-warning">
                            Ooops! Something went wrong
                        </div>
                        <div
                            v-if="weatherInfo?.message"
                            class="error-message text-danger"
                        >
                            {{ capitalizeFirstLetter(weatherInfo?.message) }}
                        </div>
                    </div>
                    <slot></slot>
                </div>

                <slot name="description"></slot>
                <!-- <div v-once="!isError">
                    <div
                        class="spinner-border text-warning d-flex mx-auto"
                        style="width: 3rem; height: 3rem"
                        role="status"
                    ></div>
                </div> -->
            </div>
        </div>
    </main>
</template>

<style lang="scss">
.wrapper {
    min-height: 100vh;
}
.main-content {
    display: grid;
    gap: 1rem;
    @media screen and (min-width: 992px) {
        grid-template-columns: 4fr 8fr;
    }
    &__error {
        @media screen and (min-width: 992px) {
            grid-template-columns: 1fr;
        }
    }
}
</style>
