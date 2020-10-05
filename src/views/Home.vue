<template>
    <main>
        <Background :data="time" />
        <div class="wrapper">
            <SearchInput v-model:searchValue="searchValue" @input="weatherData" :class="{ error: error }"/>

            <transition name="fade" mode="out-in">
                <Introduction v-if="!step" />

                <Weather v-else :data="weather.data" />
            </transition>
        </div>
    </main>
</template>

<script>
import Background from '@/components/Background.vue';
import SearchInput from '@/components/SearchInput.vue';
import Introduction from '@/components/Introduction.vue';
import Weather from '@/components/Weather.vue';

import debounce from 'lodash.debounce';
import axios from 'axios';
import { ref } from 'vue';

export default {
    name: 'Home',
    components: {
        Background,
        SearchInput,
        Introduction,
        Weather,
    },
    setup() {
        let step = ref(0);
        let searchValue = ref('');
        let time = ref(new Date().getHours());
        let weather = ref({});
        let error = ref(false);

        const url_base = 'https://api.openweathermap.org/data/2.5/';

        let weatherData = debounce(() => {
            if (searchValue.value === '' || searchValue.value === null) {
                step.value = 0;
            } else {
                axios.get(`${url_base}weather?q=${searchValue.value}&units=metric&appid=31a5730cdf6061bce8911ad865cf481d`)
                    .then((res) => {
                        if (error.value) error.value = false;
                        weather.value = res;
                        step.value = 1;
                        updateTime();
                    })
                    .catch(() => {
                        error.value = true;
                    });
            }
        }, 500);

        function updateTime() {
            const offset = weather.value.data.timezone / 3600;
            let today = new Date();
            const utc = today.getTime() + (today.getTimezoneOffset() * 60000);
            today = new Date(utc + (3600000 * offset));
            time.value = today.getHours();
        }

        return { step, searchValue, time, error, url_base, weather, weatherData };
    }
};
</script>

<style lang="scss" scoped>
    main {
        width: 100%;
        height: 100%;
        min-height: 100%;
        position: relative;

        @media (min-width: 600px) {
            & {
                display: flex;
                justify-content: center;
                align-items: center;
            }
        }
    }
    .wrapper {
        width: 100%;
        height: 100%;
        max-width: 600px;

        @media (min-width: 1024px) {
            & {
                display: flex;
                flex-direction: column;
                justify-content: center;
            }
        }
    }

    /* Animation */
    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }
    .fade-enter-from, .fade-leave-to {
        opacity: 0;
    }
</style>