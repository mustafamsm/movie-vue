<template>
    <div class="movie-detail">
        <h2>{{ movie.Title }}</h2>
        <p>{{ movie.Year }}</p>
        <p class="genre">{{ movie.Genre }}</p>
        <img :src="movie.Poster" alt="movie poster" class="featured-img" />
        <p class="plot">{{ movie.Plot }}</p>

    </div>
</template>

<script setup>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import env from '@/env.js'
const movie = ref({})
const route = useRoute()

onBeforeMount(() => {
    fetch(`http://www.omdbapi.com/?i=${route.params.id}&apikey=${env.apiKey}&plot=full`)
        .then(res => res.json())
        .then(data => {
            movie.value = data
        })
})
</script>
<style lang="scss">
.movie-detail {
    padding: 26px;
    h2{
        color:#fff;
        font-size: 28px;
        font-weight: 600;
        margin-bottom: 16px;

    }
    .featured-img{
        display: block;
        max-width: 200px;
        margin-bottom: 16px;
    }
    p{
        color: #fff;
        font-size: 18px;
        line-height:1.4 ;
    }
}
 
</style>


