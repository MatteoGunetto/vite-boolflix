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
            else if (lang == 'el') {
                return classflag = 'gr'
            }
            return classflag = lang
        },
        cover(posterpath){
            return `https://image.tmdb.org/t/p/w342/${posterpath}`
            
        },
        voteAndStars(OldValue){
            let NewValue = ((OldValue - 2 ) *0.5) +1
            if (OldValue == 0) {
                return this.stars = 0
            }
            return this.stars = parseInt(NewValue.toFixed(0));
        }
    }
    }
</script>
    <template>
        <main>
            <section>
                <!-------- SECTION FILM -------->
                <div class="title-container">
                    <div>
                        <h4>FILM</h4>
                    </div>
                </div>
                <!-- card film -->
                <div class="my-container">
                <div v-for="element in store.movies" class="flip-card">
                    <div class="flip-card-inner">
                        <div class="flip-card-front">
                            <img :src="cover(element.poster_path)" :alt="element.original_title">
                        </div>
                        <div class="description flip-card-back">
                            <div>
                                <p>
                                    <strong>Titolo: </strong>
                                    <span class="caption">
                                        {{ element.title }}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Titolo originale: </strong>
                                    <span class="caption">
                                        {{ element.original_title }}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Lingua: </strong>
                                    <span class="caption" :class="'fi fi-' + setFlag(element.original_language)"></span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Trama: </strong>
                                    <span> 
                                        {{ element.overview}}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Voto: </strong>
                                    <span v-for="index in voteAndStars(element.vote_average)">
                                        <font-awesome-icon icon="fa-solid fa-star" style="color: #ffd500;" />
                                    </span>
                                    <span v-for="index in (5 - voteAndStars(element.vote_average))">
                                        <font-awesome-icon class="icon-star" icon="fa-regular fa-star" />
                                    </span>
                                </p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
                <!-------- SECTION SERIE TV -------->
                <div class="title-container">
                    <div>
                        <h4>SERIE TV</h4>
                    </div>
                </div>
                <!-- serie tv card -->
                <div class="my-container">
                <div v-for="elementB in store.series" class="flip-card">
                    <div class="flip-card-inner">
                        <div class="flip-card-front">
                            <img :src="cover(elementB.poster_path)" :alt="elementB.original_title">
                        </div>
                        <div class="description flip-card-back">
                            <div>
                                <p>
                                    <strong>Titolo: </strong>
                                    <span class="caption">
                                        {{ elementB.name }}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Titolo originale: </strong>
                                    <span class="caption">
                                        {{ elementB.original_name }}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Lingua: </strong>
                                    <span class="caption" :class="'fi fi-' + setFlag(elementB.original_language)"></span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Trama: </strong>
                                    <span> 
                                        {{ elementB.overview}}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <p>
                                    <strong>Voto: </strong>
                                    <span v-for="index in voteAndStars(elementB.vote_average)">
                                        <font-awesome-icon icon="fa-solid fa-star" style="color: #ffd500;" />
                                    </span>
                                    <span v-for="index in (5 - voteAndStars(elementB.vote_average))">
                                        <font-awesome-icon class="icon-star" icon="fa-regular fa-star" />
                                    </span>
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            </section>
        </main>
    </template>

<style lang="scss" scoped>
@use "../styles/general.scss" as *;
@use "../styles/cardHover.scss" as *;
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
    main{
        height: 90vh;
        overflow-y: auto;
        padding: 20px 0;
        background-color: rgb(41, 40, 40);
    }
    h4{
        font-size: 30px;
    }
    .title-container{
        padding: 15px 0;
        color: white;
        background-color: black;
        margin: 15px 0;
        &>div{
            width: 90vw;
            margin: 0 auto;
        }
    }
    p{
        font-size: 16px;
        line-height: 20px;
        margin-bottom: 10px;
    }
    strong{
        color: red;
    }
    .my-container{
        width: 90vw;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        gap: 40px;
    }
    div.description{
        position: absolute;
        max-width: 342px;
        background: rgba(0, 0, 0, 0.514);
        color: white;
        padding: 5px 5px 0 5px;
        border: 2px white solid;
        overflow: hidden;
    }
    
</style>