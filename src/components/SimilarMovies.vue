<template>
    <div class="trending-wrapper animate__animated animate__fadeInUp animate__delay-1s">
        <div class="grid-container-xxl">
            <div class="trending-title">Similar Movies</div>
        <div class="trending-movies-container">
            <div class="movie-wrapper">
                
                <div class="movie-container" v-for="movie in movies" :key="movie.id">
                <router-link v-on:click="reloadPage()" :to="'/movie/' + movie.id">
                <div class="movie-rating">{{ movies.vote_average.slice(0,4) }}</div>
                <div class="poster-image">
                    <img :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`">
                </div>
                <div class="movie-title text-left">{{ movie.title }}</div>
                </router-link>
                </div>  
                        
                </div>
        </div>
        </div>
    </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
    setup() {
        const movies = ref ({});
        const route = useRoute();
        
        onBeforeMount(() => {
            //fetch movie
            fetch(`https://api.themoviedb.org/3/movie/${route.params.id}/similar?api_key=${env.apikey}`)
                .then(response => response.json())
                .then(data => {
                movies.value = data.results;
                console.log(movies.value);
                });
        });
        return {
            movies
        }
    }
}
</script>

<style scoped>
.trending-wrapper {
    margin-top: 75px;
}

.trending-wrapper::-webkit-scrollbar-thumb {
    background: var(--accentColor);
}

.trending-movies-container {
    height: 380px;
    /* background: red; */
}

.movie-wrapper {
    display: flex;
    overflow-x: scroll;
    height: auto;
    width: 97%;
}

.movie-rating {
    position: relative;
    top: 310px;
    left: 170px;
    color: var(--bgColor);
    font-weight: 700;
    width: 45px;
    height: 45px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 100%;
    background: var(--accentColor);
    box-shadow: 0px 9px 15px -6px rgba(100,217,138,0.29);
}

.movie-wrapper::-webkit-scrollbar {
    height: 5px;
}

.movie-wrapper::-webkit-scrollbar-track {
    background: var(--bgColor);
    border-radius: 10px;
}

.movie-wrapper::-webkit-scrollbar-thumb {
    background: var(--otherColor);
    border-radius: 10px;
}


.movie-container {
    margin-right: 20px;
    display: block;
    transition: transform 0.1s;
}

.movie-container img {
    object-fit: auto;
}

.trending-title {
    font-size: 28px;
    color: var(--accentColor);
    font-weight: 700;
    margin-bottom: -15px;
}

.poster-image {
    height: 300px;
    width: 200px;
    border-radius: 20px;
    background: gray;
    object-fit: cover;
    background-size: contain;
    background-repeat: no-repeat;
}

.poster-image img {
    height: 300px;
    width: 200px;
    object-fit: cover;
    border-radius: 20px;
}

.movie-title {
    width: 200px;
    font-size: 18px;
    font-weight: 600;
    color: white;
    margin-top: 10px;
    transition: color 0.1s;
}

.movie-title:hover {
    color: var(--accentColor);
}

.slide-fader {
    position: sticky;
    left: 1231px;
}



</style>