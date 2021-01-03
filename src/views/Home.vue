<template>
  <div class="home">
    <div class="feature-card">
      <img src="https://variety.com/wp-content/uploads/2020/05/netflix-logo.png" alt="Netflix" class="featured-img">
      <div class="detail">
        <h3>영화 검색하기</h3>
      </div>
    </div>
    
    <form @submit.prevent="SearchMovies()" class="search-box"> <!-- preventDefault와 같은 속성 -->
      <input type="text" placeholder="찾으시는 영화를 입력해주세요." v-model="moviesearch">
      <input type="text" placeholder="찾으시는 연도를 입력해주세요." v-model="yearsearch">
      <input type="submit" value="Search">
    </form>
    
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

export default {
  setup () { // https://leestrument.tistory.com/entry/setup 기존에 data, methods 등으로 흩어져있던것을, 하나의 장소로 모으게 해준다.
    const moviesearch = ref("");
    const yearsearch = ref("");
    const movies = ref([]);
    
    const SearchMovies = () => {
      if (moviesearch.value != "") {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${moviesearch.value}&y=${yearsearch.value}`) // api data를 가져오는법
          .then(response => response.json())
          .then(data => {
            moviesearch.value = "";
            yearsearch.value = "";
            movies.value = data.Search;
            console.log(data.Search);
          });
      } else {
        alert("영화제목을 반드시 입력해주세요.")
      }
    };
    
    return {
      moviesearch,
      yearsearch,
      movies,
      SearchMovies,
    }
  }
}
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;
    
    .featured-img {
      width: 100%;
      display: block;
      object-fit: cover;
    }
    
    .detail {
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      
      h3 {
        color: #fff;
        text-align: center;
      }
        
      p {
        color: #fff;
        font-size: 13px;
      }
    }
  }
  
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 50px 16px 16px;
    
    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      
      &[type="text"] {
        width: 100%;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;
        
        &::placeholder {
          color: #f3f3f3;
        }
        
        &:focus {
          box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
        }
      }
      
      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42B883;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        
        &:active {
          background-color: #3B8070;
        }
      }
    }
  }
  
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0 8px;
    
    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
      
      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        
        .product-image {
          position: relative;
          display: block;
          
          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }
          
          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #fff;
            bottom: 16px;
            left: 0;
            text-transform: capitalize;
          }
        }
        
        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year {
            color: #AAA;
            font-size: 14px;
          }
          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
} 
</style>