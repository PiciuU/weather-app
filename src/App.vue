<template>
    <router-view />
</template>

<style lang="scss">
    @font-face {
        font-family: "Montserrat";
        src: url("assets/fonts/Montserrat-Regular.ttf");
    }
    #app {
        font-family: 'Montserrat', sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }
    html, body, #app {
        width: 100%;
        height: 100%;
        min-height: 100%;
    }
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }
</style>
