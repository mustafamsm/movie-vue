<script setup>
import { RouterLink } from 'vue-router'

import { ref } from 'vue'
import env from '@/env.js'

const search = ref('')
const movies = ref([])
const looding=ref(false)

const SearchMovies = () => {

  if (search.value != '') {
    looding.value=true
    fetch(`http://www.omdbapi.com/?s=${search.value}&apikey=${env.apiKey}`)
      .then(res => res.json())
      .then(data => {
        looding.value=false
        movies.value = data.Search
        search.value = ''
      })
  }
}
</script>

<template >
  <div class="home">

  
    <div class="feature-card">
      <RouterLink to="/movie/tt3896198">
        <img
          src="https://m.media-amazon.com/images/M/MV5BNjM0NTc0NzItM2FlYS00YzEwLWE0YmUtNTA2ZWIzODc2OTgxXkEyXkFqcGdeQXVyNTgwNzIyNzg@._V1_SX300.jpg"
          alt="Guardians of the Galaxy Vol. 2" class="featured-img">
        <div class="detail">
          <h3>Guardians of the Galaxy Vol. 2</h3>
          <p>
            The Guardians struggle to keep together as a team while dealing with their personal family issues, notably
            Star-Lord's encounter with his father, the ambitious celestial being Ego.
          </p>
        </div>
      </RouterLink>
    </div>

    <form @submit.prevent="SearchMovies" class="search-box">
      <input type="text" placeholder="What are you looking for ?" v-model="search">
      <input type="submit" value="search">
    </form>
    <div class="looding" v-if="looding">
      <div class="lds-ripple">looding----</div>

    </div>

    <div class="movies-list" >
      <div class="movie " v-for="movie in movies" :key="movie.imdbID">
        <RouterLink :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" :alt="movie.Title">
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </RouterLink>

      </div>

    </div>

  </div>
</template>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      .h3 {
        color: #fff;
        margin-bottom: 16px;
      }

      p {
        color: #fff;

      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

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
        border-radius: 15px;
        transition: 0.04s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);

        }
      }

      &[type="submit"] {

        width: 100%;
        max-width: 300px;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 16px;
        border-radius: 15px;
        transition: 0.4s;
        margin-top: 16px;
        text-transform: uppercase;
        cursor: pointer;

        &:active {
          background-color: #3a4e6e;
        }
      }
    }
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

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
            left: 0px;
            text-transform: capitalize;

          }
        }

        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
        }

        .year {
          color: #AAA;
          font-size: 14px;

        }

        h3 {
          color: #fff;
          font-size: 18px;
          font-weight: 600;
        }


      }
    }
  }
}
</style>
