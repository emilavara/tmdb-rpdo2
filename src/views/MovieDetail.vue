<template>
<div>
<Nav/>
<div class="animate__animated animate__fadeInUp wrapper">
    <div id="trailer-modal" v-if="show" v-on:click="show = false">
        <div class="trailer-container">
            <iframe width="720" height="405" :src="`https://www.youtube.com/embed/${trailerKey}`" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            <div class="close-btn" v-on:click="show = false"><span>&#10005;</span></div>
        </div>
    </div>
    <div class="movie-container">
        <div class="grid-container-xxl">
            <div class="grid-row">
                <div class="gs-6 movie-poster">
                    <img :src="`https://image.tmdb.org/t/p/original/${movie.backdrop_path}`">
                </div>
                <div class="gs-6 movie-details">
                    <div class="movie-title">{{ movie.title }} <span class="movie-year">({{movie.release_date.slice(0, 4)}})</span></div>
                    <div class="movie-rating-and-genre-container">
                        <div class="movie-rating">
                            <span class="star">★</span> {{movie.vote_average}}<span class="grayText"> / 10</span>
                        </div>
                        <div class="movie-genre">
                            <span>{{ movieGenres.name }}</span>
                        </div>
                    </div>
                    <div class="movie-overview">{{ movie.overview }}</div>
                    <div class="trailer-button" v-on:click="show = true">See Trailer</div>
                </div>
            </div>
        </div>
    </div>
    <Actors/>
    <TrendingMovies v-on:click="reloadPage()"/>
    
</div>
</div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
import Actors from '@/components/Actors.vue';
import TrendingMovies from '@/components/TrendingMovies.vue';
import Nav from '@/components/Nav.vue'

export default {
    data: function() {
        return {
        show: false
    }
    },
    name: 'MovieDetail',
    props: ["id"],
    components: {
        Actors,
        TrendingMovies,
        Nav
    },
            methods: {
        reloadPage(){
            window.location.reload();
            scroll(0,0);
        }
        },
    setup() {
        const movie = ref ({});
        const movieGenres = ref ([]);
        const trailerKey = ref({})
        const route = useRoute();
        
        onBeforeMount(() => {
            //fetch movie
            fetch(`https://api.themoviedb.org/3/movie/${route.params.id}?api_key=${env.apikey}&append_to_response=videos`)
                .then(response => response.json())
                .then(data => {
                movie.value = data;
                trailerKey.value = data.videos.results[0].key;
                movieGenres.value = data.genres[0];
                console.log(movieGenres.value);
                });
        });
        return {
            movie,
            trailerKey,
            movieGenres
        }
    }
}
</script>

<style scoped>

#trailer-modal {
    height: 200vh;
    width: 99.6vw;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 2;
    background: rgba(8, 29, 37, 0.97);
    display: flex;
    justify-content: center;
    padding-top: 150px;
    animation: fadeIn 0.2s;
}

.movie-rating-and-genre-container {

}

.trailer-container {
    width: 720px;
    height: 405px;
    border-radius: 20px;
    position: relative;
}

.trailer-container iframe {
    border-radius: 20px;
}

.trailer-container img {
    width: 720px;
    height: 405px;
    border-radius: 20px;
    object-fit: contain;
}

.close-btn span {
    top: -35px;
    right: -35px;
    position: absolute;
    color: var(--accentColor);
    font-size: 22px;
    padding: 2px 5px;
    background: rgba(255, 255, 255, 0.116);
    border-radius: 5px;
    cursor: pointer;
    font-weight: 800;
}

@keyframes fadeIn {
    from {opacity: 0}
    to {opacity: 1}
}

.movie-container {
    padding: 100px 0;
    height: auto;
    background: var(--otherColor);
    display: grid;
    z-index: 1;
}

.movie-poster {
    height: 25rem;
    width: 37.5rem;
    border-radius: 20px;
}

.movie-poster img {
    height: 25rem;
    width: 37.5rem;
    object-fit: cover;
    border-radius: 20px;
}

.movie-details {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    gap: 20px;
    height: 400px;
}

.movie-rating {
    margin-bottom: 20px;
    color: white;
    font-weight: 700;
    font-size: 24px;
    float: left;
}

.movie-genre {
    font-size: 24px;
    float: right;
    font-weight: 700;
    color: var(--accentColor);   
}

.star {
    color: #FFD700;
}

.movie-title {
    font-size: 2.75rem;
    color: var(--accentColor);
    font-weight: 700;
}

.movie-overview {
    font-size: 1rem;
    color: white;
    font-weight: 600;
    line-height: 26px;
    position: relative;
    bottom: 20px;
}

.movie-year {
    font-size: 1.5rem;
    color: white;
    position: relative;
    bottom: 7px;
    left: 5px;
}

.trailer-button {
    background: var(--accentColor);
    width: 160px;
    height: 65px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 18px;
    font-weight: 700;
    border-radius: 14px;
    cursor: pointer;
    user-select: none;
    box-shadow: 0px 9px 15px -6px rgba(100,217,138,0.29);
}

.bg {
    background: red;
}

@media only screen and (max-width: 375px) 
{ 
    .movie-container {
        padding: 250px 0;
    }
    .movie-poster {
        width: 200px;
        height: 110px;
        margin-bottom: 40px;
        margin-top: -20px;
    }

    .movie-poster img {
        width: 87vw;
        height: 210px;
    }

    .movie-overview {
        margin-bottom: 40px;
    }

    .movie-title {
        font-size: 32px;
        margin-top: 90px;
    }

    .movie-overview {
        margin-top: 80px;
    }
    
    .movie-details {
        height: auto;
    }
}
</style>