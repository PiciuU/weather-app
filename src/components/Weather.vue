<template>
    <div class="container">
        <div class="location">
            <div class="location__title">{{ data.name }}, {{ data.sys.country }}</div>
            <div class="location__date">{{ fetchDate() }}</div>
        </div>

        <div class="card">
            <div class="card__inner">
                <div class="card__front">
                    <div class="card__title">{{ Math.round(data.main.temp) }}°C</div>
                    <div class="card__icon"><img :src="`http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`"></div>
                </div>
                <div class="card__back">
                    <div class="card__description">{{ data.weather[0].main }}</div>
                </div>
            </div>
        </div>

        <div class="card card--reversed">
            <div class="card__inner">
                <div class="card__front">
                    <div class="card__title card__title--minimum"><img src="@/assets/icons/temp-min.svg">{{ Math.round(data.main.temp_min) }}°C</div>
                    <div class="card__title card__title--maximum"><img src="@/assets/icons/temp-max.svg">{{ Math.round(data.main.temp_max) }}°C</div>
                </div>
                <div class="card__back">
                    <div class="card__description">Min & Max Temp</div>
                </div>
            </div>
        </div>

        <div class="card">
            <div class="card__inner">
                <div class="card__front">
                    <div class="card__title card__title--humidity"><img src="@/assets/icons/humidity.svg" title="Humidity" alt="Humidity Icon">{{ data.main.humidity }}%</div>
                </div>
                <div class="card__back">
                    <div class="card__description">Humidity</div>
                </div>
            </div>
        </div>

        <div class="card card--reversed">
            <div class="card__inner">
                <div class="card__front">
                    <div class="card__title card__title--pressure"><img src="@/assets/icons/pressure.svg" title="Pressure" alt="Pressure Icon">{{ data.main.pressure }} Pa</div>
                </div>
                <div class="card__back">
                    <div class="card__description">Pressure</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Weather",
    props: {
        data: {
            type: Object,
            required: true,
        },
    },
    setup(props) {
        function fetchDate() {
            const offset = props.data.timezone / 3600;
            let today = new Date();
            const utc = today.getTime() + (today.getTimezoneOffset() * 60000);
            today = new Date(utc + (3600000 * offset));
            const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
            const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
            const day = days[today.getDay()];
            const date = today.getDate();
            const month = months[today.getMonth()];
            const year = today.getFullYear();
            let hour = today.getHours();
            hour = (`0${hour}`).slice(-2);
            let min = today.getMinutes();
            min = (`0${min}`).slice(-2);

            return `${day} ${date} ${month} ${year} ${hour}:${min}`;
        }
        return { fetchDate };
    },
}
</script>

<style lang="scss" scoped>
    .location {
        text-align: center;

        &__title {
            color: white;
            font-size: 38px;
            font-weight: bold;
            text-shadow: 1px 3px rgba(0, 0, 0, .35);
            margin-bottom: 5px;
        }

        &__date {
            color: white;
            font-size: 22px;
            font-style:italic;
            padding: 0px 5px;
        }
    }

    .card {
        margin: 20px;
        padding: 10px;
        background: rgba(15,15,15,.4);
        box-shadow: 5px 5px rgba(255, 255, 255, .25);
        border-radius: 10px;
        color: white;
        text-align: center;
        transition: all .5s ease-in-out;

        &--reversed {
            box-shadow: -5px 5px rgba(255, 255, 255, 0.25);
        }

        &:hover &__inner {
            transform: rotateY(180deg);
        }

        &__inner {
            display: flex;
            flex-direction: row;
            justify-content: center;
            align-items: center;
            width: 100%;
            min-height: 60px;
            transition: transform .6s ease-in-out;
            transform-style: preserve-3d;

            img {
                width: 50px;
                height: 50px;
            }
        }

        &__front, &__back {
            display: flex;
            flex-direction: row;
            justify-content: center;
            align-items: center;
            position: absolute;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            z-index: 1;
        }

        &__back {
            transform: rotateY(180deg);
        }

        &__description {
            color: white;
            font-size: 48px;
        }

        &__title {
            font-size: 48px;
            font-weight:bold;
            text-shadow: 2px 5px rgba(0, 0, 0, .35);
            letter-spacing: 1px;

            &--minimum {
                display: flex;
                align-items: center;
                padding:0px 10px;
                color: rgb(121, 152, 219);
            }

            &--maximum {
                display: flex;
                align-items: center;
                padding:0px 10px;
                color: rgb(228, 27, 27);
            }

            &--humidity, &--pressure {
                font-size: 48px;
                font-weight:bold;
                text-shadow: 2px 5px rgba(0, 0, 0, .35);
                letter-spacing: 1px;
                display: flex;
                align-items: center;
                img {
                    margin-right:20px;
                }
            }
        }

        &__icon {
            margin-left: 40px;
            margin-top:4px;
            img {
                transform:scale(1.5);
            }
        }

        @media (max-width: 767px) {
            &__description {
                font-size:32px;
            }
        }

        @media (max-width:400px) {
            &__title--minimum, &__title--maximum {
                font-size: 36px;
            }
        }

        @media (max-width:359px) {
            &__title--minimum, &__title--maximum {
                font-size: 32px;
                padding: 0px 5px;
            }

            &__title--humidity, &__title--pressure {
                font-size: 42px;
            }
        }
    }
</style>