<template>
  <div class="container movie-detail">
    <div class="poster-movie">
      <img :src="movie.Poster" alt="">
    </div>
    <h1>{{ movie.Title }}</h1>
    <p>{{ movie.Plot }}</p>
    <br>
    <div class="details">
      <p>Writer: {{ movie.Writer }}</p>
      <p>Actors: {{ movie.Actors }}</p>
      <p>Country: {{ movie.Country }}</p>
      <p>Genre: {{ movie.Genre}}</p>
      <p>Language: {{ movie.Language }}</p>
      <p>Released: {{ movie.Released }}</p>
      <p>Runtime: {{ movie.Runtime }}</p>
      <p>Year: {{ movie.Year }}</p>
      <p>Rating: {{ movie.imdbRating }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import env from '../env.js'

export default {
  setup() {
    const movie = ref({})
    const route = useRoute()

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data
        })
    })

    return {
      movie
    }
  }
};
</script>

<style scoped>
  .container.movie-detail {
    padding: 40px;
  }

  .poster-movie {
    display: flex;
    justify-content: center;
  }

  h1 {
    text-align: center;
    margin: 10px;
    font-size: 2.5rem;
    font-weight: 700;
  }

  .details p {
    margin: 10px 0;
    font-weight: 700;
  }
</style>
