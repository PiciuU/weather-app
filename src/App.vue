<template>
    <div id="app">
        <router-view/>
    </div>
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
        background-image: url('./assets/imgs/bg-mountains.png');
        background-size: cover;
        background-position: bottom;
        transition: .3s;
    }

    html, body, #app {
        width: 100%;
        height: 100%;
    }

    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

</style>
