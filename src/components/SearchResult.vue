<template>
    <div class="search-result-wrapper animate__animated animate__fadeInUp">
        <div class="search-result-title">Search Results</div>
        <div class="search-result-movies-container">
            <div class="movie-wrapper">
                <div class="movie-container" v-for="movie in movies" :key="movie.id">
                <router-link v-on:click="reloadPage()" :to="'/movie/' + movie.id">
                <div class="movie-rating">{{ movie.vote_average }}</div>
                <div class="poster-image">
                    <img :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"/>
                </div>
                <div class="movie-title text-left">{{movie.title}}</div>
                </router-link>
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
        const movies = ref ([]);
        const route = useRoute();
        
        onBeforeMount(() => {
            //fetch movie
            fetch(`https://api.themoviedb.org/3/search/movie?api_key=${env.apikey}&query=${route.params.query}`)
                .then(response => response.json())
                .then(data => {
                movies.value = data.results;
                console.log(movies.value);
                });
        });
        return {
            movies
        }
    },
    methods: {
        reloadPage() {
            scroll(0,0);
        }
    }
}
</script>

<style scoped>
.search-result-wrapper {
    background: var(--otherColor);
    padding-bottom: 50px;
}

.movie-wrapper {
    display: flex;
    flex-flow: row wrap;
    padding-left: 50px;
}


.movie-container {
    margin-right: 20px;
    margin-bottom: 0px;
    cursor: pointer;
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

.search-result-title {
    font-size: 28px;
    color: var(--accentColor);
    font-weight: 700;
    padding-top: 50px;
    padding-left: 50px;
}

.poster-image {
    height: 300px;
    width: 200px;
    border-radius: 20px;
}

.poster-image img {
    height: 300px;
    width: 200px;
    border-radius: 20px;
    object-fit: contain ;
}

.movie-title {
    width: 200px;
    font-size: 18px;
    font-weight: 600;
    color: white;
    margin-top: 10px;
}

.movie-title:hover {
    color: var
}
</style>