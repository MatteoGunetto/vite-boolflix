<script>
    import axios from 'axios';
    import AppSearch from "./AppSearch.vue";
    import { store } from '../store';
    export default {
        name: 'AppHeader',
        components: {
            AppSearch
        },
        data() {
            return{
                store
            }
        },
        methods:{
            titleSearch(){
                axios.get('https://api.themoviedb.org/3/search/movie',{
                    params:{
                        api_key: '1725aa60ed5d2ef0f1559236ce1f53b3',
                        query: this.store.searchText,
                        language: 'it-IT'}
                    }
                )
                .then((response) => {
                    console.log('ricerca: ', this.store.searchText, response.data.results)
                    this.store.movies = response.data.results
                })
            }
        }
    }
</script>

<template>
    <h1>BoolFlix</h1>
    <AppSearch @search="titleSearch"/>
</template>

<style lang="scss">
</style>