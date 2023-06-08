<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
export default {
    name: 'App',
    components: {
        AppHeader,
        AppMain,
    },
    data() {
        return {
        }
    }
}
</script>
<template>

    <AppHeader />
    <AppMain />

</template>

<style lang="scss">
@use "./styles/general.scss" as *;
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
body{
    font-family: "Bebas Neue";
}
</style>