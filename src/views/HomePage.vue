<template>
<div>
<NavAlt/>
    <div>
        <div class="blob">
            <img src="../img/blobs.svg">
        </div>
        <div class="text-container">
            <div class="big-text">TMDb</div>
            <div class="small-text">The <span class="accentText">modern</span> movie database</div>
        </div>
        <div class="form-container animate__animated animate__fadeInUp">
            <form @submit.prevent="searchMovies()" class="search-box">
                <input type="text" v-model="search" id="" class="search-box" placeholder="Search Movies...">
            </form>
        </div>
        <TrendingMovies/>
        <TopRated/>
    </div>
</div>
</template>

<script>
import TrendingMovies from '@/components/TrendingMovies.vue'
import TopRated from '@/components/TopRated.vue'
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import NavAlt from '@/components/NavAlt.vue'

export default {
    name: 'HomePage',
    components: {
    TrendingMovies,
    TopRated,
    NavAlt
    },
    setup() {
        const search = ref("");
        const router = useRouter();
        
        const searchMovies = () => {
            if (search.value != "") {
                router.push('/search/' + search.value)
                search.value = "";
            }
        }
        return {
            search,
            searchMovies
        }
    }
}
</script>

<style scoped>
.blob {
    position: absolute;
    top: -50px;
    left: -50px;
}

.big-text {
    font-size: 80px;
    font-weight: 800;
    color: var(--accentColor);
    text-align: center;
}

.small-text {
    font-size: 40px;
    font-weight: 700;
    color: white;
    text-align: center;
}

.text-container {
    margin-top: 50px;
}

.search-box {
    display: block;
    margin: auto;
    border: none;
    height: 60px;
    width: 475px;
    border-radius: 20px;
    margin-top: 50px;
    background: var(--otherColor);
    color: white;
    font-size: 22px;
    font-weight: 600;
    padding-left: 20px;
    position: relative;
    right: 10px;
}

input:focus,
select:focus,
textarea:focus,
button:focus {
    outline: none;
}

::placeholder {
    color: white;
    opacity: 0.2;
}


@media only screen and (max-width: 600px) {
    .text-container {
        margin-top: 150px;
    }
    .search-box {
        width: 300px;
    }
    
    .movie-wrapper {
        width: 126vw;
    }

    .blob {
        display: none;
    }
}
</style>