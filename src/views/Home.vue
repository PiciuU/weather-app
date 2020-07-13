<template>
    <main>
        <div class="search-container">
            <SearchInput v-model="searchValue" @input="getWeather"></SearchInput>
        </div>

        <div class="weather-container" v-if="weather.data != undefined">
            <div class="location-box">
                <div class="location">{{ weather.data.name }}, {{ weather.data.sys.country }}</div>
                <div class="date">{{ dateCreator() }}</div>
            </div>

            <div class="weather-box">
                <div class="temp">{{ Math.round(weather.data.main.temp) }}°c</div>
                <div class="icon"><img :src="weatherStatus"></div>
            </div>
        </div>

    </main>
</template>

<script>
import SearchInput from '@/components/SearchInput.vue';
import debounce from 'lodash.debounce';
import axios from 'axios';

export default {
    name: 'Home',
    components: {
        SearchInput,
    },
    data() {
        return {
            step: 0,
            searchValue: '',

            api_key: 'dcbcc78c70ce850f14cd2a1e49385b4b',
            url_base: 'https://api.openweathermap.org/data/2.5/',
            weather: {},
        };
    },
    computed: {
        weatherStatus() {
            switch (this.weather.data.weather[0].main) {
            case 'Rain':
                return require('@/assets/icons/004-rainy-1.svg');
            case 'Drizzle':
                return require('@/assets/icons/003-rainy.svg');
            case 'Clouds':
                return require('@/assets/icons/011-cloudy.svg');
            case 'Snow':
                return require('@/assets/icons/031-snowflake.svg');
            case 'Clear':
                return require('@/assets/icons/039-sun.svg');
            case 'Thunderstorm':
                return require('@/assets/icons/045-thunder.svg');
            default:
                return require('@/assets/icons/015-day.svg');
            }
        },
    },
    methods: {
        getWeather: debounce(function () {
            axios.get(`${this.url_base}weather?q=${this.searchValue}&units=metric&appid=${this.api_key}`)
                .then((res) => {
                    this.weather = res;
                    console.log(res.data.weather[0].main);
                });
        }, 500),

        dateCreator() {
            const today = new Date();
            const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
            const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
            const day = days[today.getDay()];
            const date = today.getDate();
            const month = months[today.getMonth()];
            const year = today.getFullYear();
            return `${day} ${date} ${month} ${year}`;
        },

        timeCreator() {
            const offset = this.weather.data.timezone / 3600;
            const d = new Date();
            const utc = d.getTime() + (d.getTimezoneOffset() * 60000);
            const nd = new Date(utc + (3600000 * offset));
            console.log(nd.toLocaleString());
        },
    },
};
</script>

<style lang="scss" scoped>
    main {
        width: 100%;
        min-height: 100%;
        position: relative;
        background-image: linear-gradient(to bottom, rgba(0, 0, 0, .25), rgba(0, 0, 0, .55));
    }

    .search-container {
        width: 100%;
        padding: 10px 20px;
        margin-bottom: 20px;
    }

    .location-box {
        text-align:center;

        .location {
            color: white;
            font-size: 38px;
            font-weight: bold;
            text-shadow: 1px 3px rgba(0, 0, 0, .35);
        }
        .date {
            color: white;
            font-size: 22px;
            font-style:italic;
        }
    }

    .weather-box {
        margin: 20px;
        padding: 10px;
        background: rgba(15,15,15,.35);
        box-shadow: 5px 5px rgba(255, 255, 255, 0.25);
        border-radius: 10px;
        color: white;
        text-align: center;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;

        .temp {
            font-size: 60px;
            font-weight:bolder;
            text-shadow: 2px 5px rgba(0, 0, 0, .35);
            letter-spacing: 1px;
        }

        .icon {
            margin-left: 40px;
            margin-top:10px;
            img {
                width: 50px;
                height: 50px;
            }
        }
    }

    /* Animation */

    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }
    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</style>
