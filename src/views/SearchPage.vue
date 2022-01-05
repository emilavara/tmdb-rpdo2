<template>
<div>
<Nav/>
    <div>
        <SearchResult/>

    </div>
</div>
</template>

<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import SearchResult from '@/components/SearchResult.vue'
import Nav from '@/components/Nav.vue'

export default {
    name: 'HomePage',
    components: {
    SearchResult,
    Nav
    },
    setup() {
        const searchAgain = ref("");
        const router = useRouter();
        
        const searchMovies = () => {
                router.push('/search/' + searchAgain.value)
        }
        return {
            searchAgain,
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
    margin-top: 0px;
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
    padding-left: 20px;
    font-weight: 600;
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
    .blob {
        display: none;
    }
}
</style>