<template>
    <div class="introduction">
        <div class="introduction__title">Current Weather</div>
        <div class="introduction__subtitle">Type any city for which you want to check the weather</div>
    </div>
</template>

<script>
export default {
    name: "Introduction",
}
</script>

<style lang="scss" scoped>
    .introduction {
        width:100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align:center;

        &__title {
            margin-top: 50px;
            color: white;
            font-size: 37px;
            text-shadow: 1px 3px rgba(0, 0, 0, .35);
            font-weight: bold;
            margin-bottom: 10px;
            padding: 2px;
        }

        &__subtitle {
            color: white;
            font-size: 22px;
            font-style:italic;
            padding: 2px;
        }
    }
</style>