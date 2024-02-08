<script setup>
const props = defineProps({
    cord: {
        type: Object,
        required: true,
    },
    humidity: {
        type: Number,
        required: true,
    },
});
</script>
<template>
    <section class="description py-3 rounded-4">
        <div class="description-list">
            <div class="d-lg-flex align-items-center description-item p-3">
                <div class="">
                    <img
                        src="../assets/img/compass.png"
                        alt=""
                        class="description-img d-block mx-auto"
                    />
                </div>
                <div class="description-info mx-md-4">
                    <div class="description-info-block">
                        <p class="description-land">
                            Longitude: {{ cord.lon }}
                        </p>
                        <p class="description-land-info">
                            Longitude measures distance east or west of the
                            prime meridian.
                        </p>
                    </div>
                    <div class="description-info-block">
                        <p class="description-land">Latitude: {{ cord.lat }}</p>
                        <p class="description-land-info">
                            Latitude lines start at the equator (0 degrees
                            latitude) and run east and west, parallel to the
                            equator.
                        </p>
                    </div>
                </div>
            </div>
            <div class="d-lg-flex align-items-center description-item p-3">
                <img
                    src="../assets/img/humidity.png"
                    alt=""
                    class="description-img d-block mx-auto"
                />

                <div class="description-info mx-md-4">
                    <div class="description-info-block">
                        <p class="description-land">
                            Humidity: {{ humidity }} %
                        </p>
                        <p class="description-land-info">
                            Humidity is the concentration of water vapor present
                            in the air. Water vapor, the gaseous state of water,
                            is generally invisible to the human eye.
                        </p>
                    </div>
                    <div class="description-info-block">
                        <p class="description-land-info">
                            The same amount of water vapor results in higher
                            relative humidity in cool air than warm air.
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<style lang="scss" scoped>
.description {
    &-list {
        display: grid;
        gap: 1rem;
        // margin-top: 1rem;
        @media screen and (min-width: 768px) {
            grid-template-columns: 6fr 6fr;
        }
    }
    &-item {
        background: url(../assets/img/gradient-3.jpg) no-repeat center/cover;
        border-radius: 25px;
    }
    &-img {
        max-width: 4.375rem;
    }
    &-info {
    }
}
</style>
