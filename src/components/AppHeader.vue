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
            officialResearch(){
                this.titleSearch('movie'),
                this.titleSearch('tv')
            },
            titleSearch(type){
                const mainUrl = 'https://api.themoviedb.org/3/search/'
                axios.get(mainUrl + type,{
                    params:{
                        api_key: '1725aa60ed5d2ef0f1559236ce1f53b3',
                        query: this.store.searchText,
                        language: 'it-IT'}
                    }
                )
                .then((response) => {
                    console.log('ricerca: ', this.store.searchText, response.data.results)
                    if (type == 'movie') {
                        this.store.movies = response.data.results
                    }
                    else{
                        this.store.series = response.data.results
                    }
                })
            }
        }
    }
</script>

<template>
    <section>
        <h1>BoolFlix</h1>
        <AppSearch @search="officialResearch"/>
    </section>
</template>

<style lang="scss" scoped>
@use "../styles/general.scss" as *;
section{
        @include display-flex-rule;
        align-items: center;
        height: 10vh;
        background-color: rgb(15, 15, 15);
        padding:  0 20px;
        h1{
            color: #EC2724;
            font-size: 50px;
        }
    }
</style>