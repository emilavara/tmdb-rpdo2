<template>
<div>
    <div class="grid-container-xxl">
    <div class="section-title">Cast</div>
        <div class="grid-row">
            <div class="gs-3 actor-container" v-for="cast in apiData" :key="cast.id">
                <div class="actor-img">
                    <img :src="`https://image.tmdb.org/t/p/original/${cast.profile_path}`">
                </div>
                <div class="actor-info">
                    <div class="actor-name">{{cast.name}}</div>
                    <div class="actor-character">{{ cast.character }}</div>
                </div>
            </div>           
        </div>
    </div>
</div>
</template>

<script>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';

export default {
  setup () {
    const apiData = ref([])
    const route = useRoute();

    const fetchApiData = async () => {
      await fetch(
        `https://api.themoviedb.org/3/movie/${route.params.id}/credits?api_key=a2dbcf0215153cea2c38aa62b39b4f60&language=en-US`
      )
        .then(res => res.json())
        .then(data => {
          apiData.value = data.cast.slice(0, 12)
          console.log(apiData);
        })
        .catch(err => {
          console.log(err)
        })
    }
    onMounted(fetchApiData)
    return {
      apiData
    }
  }
}
</script>

<style scoped>
.actor-container {
    width: 320px;
    height: 100px;
    border-radius: 10px;
    margin-top: 30px;
    background: var(--otherColor);
    display: flex;
    gap: 20px;
    justify-content: left;
    align-items: center;
    padding-left: 20px;
    box-shadow: var(--otherShadow);
}

.section-title {
    font-size: 28px;
    color: var(--accentColor);
    font-weight: 700;
    margin-bottom: -10px;
    margin-top: 40px;
}

.actor-img {
    height: 65px;
    width: 65px;

    border-radius: 100%;
}

.actor-img img {
    height: 65px;
    width: 65px;
    object-fit: cover;
    border-radius: 100%;
}

.actor-name {
    color: white;
    font-size: 22px;
    font-weight: 600;
}

.actor-character {
    color: white;
    opacity: 0.6;
    font-size: 16px;
    font-weight: 600;
}

@media only screen and (max-width: 600px) {
    .section-title {
        margin-bottom: 20px;
    }
    .actor-container {
        margin: 10px auto;
        width: 80%;
    }
}
</style>