<template>
    <div class="background" :style="{ backgroundImage: `url(${require('@/assets/imgs/' + background)})` }" />
</template>

<script>
import { ref, watch, onBeforeMount } from 'vue';

export default {
    name: 'Background',
    props: {
        data: {
            type: [Number, String],
            required: true,
        },
    },
    setup(props) {

        let background = ref('');

        const images = [
            {
                min: 6,
                max: 8,
                name: 'bg-sunrise.jpg',
            },
            {
                min: 9,
                max: 15,
                name: 'bg-day.jpg',
            },
            {
                min: 16,
                max: 20,
                name: 'bg-mid.jpg',
            },
            {
                min: 21,
                max: 24,
                name: 'bg-evening.jpg',
            },
            {
                min: 0,
                max: 5,
                name: 'bg-night.jpg',
            }
        ];

        onBeforeMount(() => {
            images.forEach(image => {
                if (inRange(props.data, image.min, image.max)) {
                    background.value = image.name;
                }
            });
        })

        function setImage(url) {
            let fullImage = new Image();
            fullImage.src = require(`@/assets/imgs/${url}`);
            fullImage.onload = function(){
                background.value = url;
            }
        }

        watch(() => props.data, time => {
            images.forEach(image => {
                if (inRange(time, image.min, image.max)) {
                    setImage(image.name);
                }
            });
        })

        function inRange(value, min, max) {
            if (value >= min && value <= max) return true;
            return false;
        }

        return { background, inRange };
    }
};
</script>

<style lang="scss" scoped>
    .background {
        width: 100%;
        height: 100%;
        position: fixed;
        z-index: -1;
        background-size: cover;
        background-position: center;
        background-attachment: fixed;
        transition: .3s;
        &:after {
            content: "";
            width: 100%;
            height: 100%;
            z-index: 1;
            top: 0;
            left: 0;
            position: absolute;
            background-image: linear-gradient(to bottom, rgba(0, 0, 0, .25), rgba(0, 0, 0, .45));
        }
    }
</style>