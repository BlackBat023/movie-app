<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>
      {{ movie.Plot }}
    </p>
    <p>
      <ul>
        <li>Starring: {{ movie.Actors }}.</li>
        <li>Director: {{ movie.Director }}.</li>
        <li>Rated: {{ movie.Rated }}.</li>
        <li>Runtime: {{ movie.Runtime }}.</li>
        <li>Rating: {{ movie.imdbRating }}.</li>
      </ul>
    </p>
  </div>
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
        movie.value = data;
      })
    })

    return {
      movie,
      route
    }
  }
}
</script>

<style lang="scss">

.movie-detail {
  padding: 16px;

  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
    text-align: center;

  }

  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
    margin-top: 10px;
    margin-right: auto;
    margin-left: auto;
    align-content: center;
    justify-content: center;
  }

  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
    background-color: #486583;
    border-radius: 16px;
    text-align: center;
    text-justify: distribute-all-lines;
    padding: 12px;

    ul {
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      border: 1px solid skyblue;
      font-size: 12px;
      margin: 10px;
      list-style: none;
      padding: 5%;
      
      li {
        margin: 2px;
      }
    }
  }
}

</style>