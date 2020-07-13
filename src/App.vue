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
    font-family: "Montserrat";
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

body {
    padding: 0;
    margin: 0;
    width: 100%;
    height: 100%;
}

</style>
