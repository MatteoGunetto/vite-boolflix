<script>
import { store } from '../store';
    
    export default{
    name: 'AppMain',
    data() {
        return {
            store,
        }
    },
    methods:{
        setFlag(lang){
            let classflag = '';
            if (lang == 'en') {
                return classflag = 'gb'
            }
            else if(lang == 'ja'){
                return classflag = 'jp'
            }
            else if (lang == 'ko') {
                return classflag = 'kn'
            }
            else if (lang == 'hi') {
                return classflag = 'in'
            }
            else if (lang == 'zh') {
                return classflag = 'cn'
            }
            else if (lang == 'da') {
                return classflag = 'dk'
            }
            else if (lang == 'cs') {
                return classflag = 'cz'
            }
            else if (lang == 'ka') {
                return classflag = 'ge'
            }
            return classflag = lang
        },
        cover(posterpath){
            return `https://image.tmdb.org/t/p/w342/${posterpath}`
        },
        voteAndStars(OldValue){
            let NewValue = ((OldValue - 2 ) *0.5) +1
            if (OldValue == 0) {
                console.log(typeof this.stars, this.stars)
                return this.stars = 0
            }
            console.log(this.stars)
            return this.stars = parseInt(NewValue.toFixed(0));
        }
    }
    }
</script>

<template>
    <h3> <em>La tua ricerca ha ottenuto i seguenti risultati:</em> </h3>
    <h4>FILM</h4>
    <ul v-for="element in store.movies">
        <li> <strong>Titolo: </strong>{{ element.title }}</li>
        <li> <strong>Titolo originale: </strong>{{ element.original_title }}</li>
        <img :src="cover(element.poster_path)" :alt="element.original_title">
        <li> <strong>Lingua: </strong>
            {{  }}
            <span :class="'fi fi-' + setFlag(element.original_language)"></span>
        </li>
        <li> 
            <!-- <strong>Voto: </strong>{{ element.vote_average }} // {{ voteAndStars(element.vote_average) }} -->
            <span v-for="index in voteAndStars(element.vote_average)">
                <font-awesome-icon icon="fa-solid fa-star" style="color: #ffd500;" />
            </span>
            <span v-for="index in (5 - voteAndStars(element.vote_average))">
                <font-awesome-icon icon="fa-regular fa-star" />
            </span>
        
        
        
        </li>
        <!-- hr da togliere -->
        <hr>
    </ul>
    <hr>
    <h4>SERIE TV</h4>
    <ul v-for="elementB in store.series">
        <li> <strong>Titolo: </strong>{{ elementB.name }}</li>
        <li> <strong>Titolo originale: </strong>{{ elementB.original_name }} </li>
        <img :src="cover(elementB.poster_path)" :alt="elementB.original_title">
        <li> <strong>Lingua: </strong>
            <span :class="'fi fi-' + setFlag(elementB.original_language)"></span>
        </li>
        <li> 
            <!-- <strong>Voto: </strong>{{ elementB.vote_average }} // {{ voteAndStars(elementB.vote_average) }} -->
            <span v-for="index in voteAndStars(elementB.vote_average)">
                <font-awesome-icon icon="fa-solid fa-star" style="color: #ffd500;" />
            </span>
            <span v-for="index in (5 - voteAndStars(elementB.vote_average))">
                <font-awesome-icon icon="fa-regular fa-star" />
            </span>
        </li>
        <!-- hr da togliere  -->
        <hr>
    </ul>
</template>

<style lang="scss">
@use "../src/styles/general.scss"
</style>