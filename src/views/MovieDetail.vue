<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>{{ movie.Actors }}</p>
    <p>{{ movie.imdbRating }}</p>
    <p>{{ movie.Runtime }}</p>
    <p class="plot">{{ movie.Plot }}</p>
  </div> 
  <!-- {{ $route.params.id }} router 파일에서 path: '/movie/:id' 로 호출하는 URL의 마지막 file path 부분을 가져오는 방식 -->
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup () {
    const movie = ref({});
    const route = useRoute();
    
    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data; // movie.value에 저장하고 dom에서 사용할때엔 {{movie.Title}} 이런식으로 사용
        });
    });
    
    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;
  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin: 0 auto 16px;
  }
  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
    
    &.plot {
      margin-top: 16px;
      padding: 4px 8px;
      border: 1px solid #fff;
    }
  }
}
</style>