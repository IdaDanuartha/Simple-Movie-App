<template>
  <header>
        <div class="header-img"></div>
        <div class="container-text">
            <div class="text">
                <h1>Simple Searching Movie App</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facilis ex quas quae eveniet alias reiciendis perspiciatis ad aperiam, asperiores sed, repudiandae dolorum labore quis exercitationem distinctio illum suscipit corrupti id numquam eligendi sequi. Repellat</p>
            </div>
            <form @submit.prevent="searchMovies()">
                <div class="search-box">
                    <input type="text" placeholder="Search any movie here..." v-model="inputKeyword">
                    <button type="submit">Search</button>
                </div>
            </form>
        </div>
    </header>

  <div class="container card-container">
        <div v-for="movie in moviesList" :key="movie.imdbID" class="card">
        <router-link class="link" :to="'/movie-detail/' + movie.imdbID">
            <img :src="movie.Poster">
            <div class="sub-card">
                <div class="d-flex title">
                    <h3>{{ movie.Title }}</h3>
                </div>
                
                <div class="d-flex">
                    <p>{{ movie.Type }} - {{ movie.Year }}</p>    
                </div>
            </div>
            </router-link>
        </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import env from '../env.js'

export default {
    setup() {
        const inputKeyword = ref('')
        let moviesList = ref([])
        const inputValue = inputKeyword.value

        const searchMovies = () => {
            if(inputKeyword.value != "") {
                fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${inputKeyword.value}`)
                    .then(response => response.json())
                    .then(data => {
                        console.log(data.Search)
                        moviesList.value = data.Search
                        inputKeyword.value = ''
                    })
            }
        }

        return {
            inputKeyword,
            moviesList,
            inputValue,
            searchMovies
        }
    },
    components: {}
};
</script>

<style scoped>

    /* Header style */
    .header-img {
        background: url('https://picsum.photos/1920/1080') center no-repeat;
        width: 100vw;
        height: 70vh;
        filter: brightness(40%);
    }

    .container-text {
        position: relative;
        color: #eee;
        top: -180px;
        left: 50px;
    }

    .text h1 {
        text-align: center;
        margin-bottom: 30px;
    }

    .container-text .search-box {
        position: relative;
        display: flex;
        justify-content: center;
        top: 50px;
    }

    .search-box input {
        color: #fff;
        width: 50vw;
        padding: 15px 8px;
        border-radius: 5px;
        border: 3px solid lightblue;
        background: none;
        outline: none;
        margin-right: 10px;
        font-size: 1rem;
        transition: .2s;
    }

    .search-box input::placeholder {
        color: #ddd;
    }

    .search-box input:focus {
        outline: 2px solid rgb(77, 153, 179);
        box-shadow: 5px 5px 15px rgba(77, 153, 179, 0.5);
    }

    .search-box button {
        border: none;
        color: #444;
        padding: 5px 20px;
        border-radius: 5px;
        background: lightblue;
        cursor: pointer;
        transition: .2s;
    }

    .search-box button:hover {
        box-shadow: 5px 5px 15px rgba(77, 153, 179, 0.3),
        -5px -5px 15px rgba(77, 153, 179, 0.3);
    }

    .search-box button:focus {
        outline: 2px solid rgb(77, 153, 179);
    }

    .card-container {
        display: grid;
        grid-template-columns: repeat(3, minmax(100px, 1fr));
    }

    .card {
        border: 1px solid #ddd;
        border-radius: 8px;
        width: 300px;
        height: 400px;
        margin: 20px;
    }

    .card img {
        width: 100%;
        height: 300px;
    }

    .sub-card h2 {
        padding: 10px;
        text-align: center;
        margin-bottom: 2px;
    }

    .sub-card p {
        font-size: 0.8rem;
        margin: 0 10px;
    }

    .d-flex {
        display: flex;
        justify-content: center;
    }

    .d-flex.title {
        margin: 5px 15px 10px;
        font-weight: 700;
    }
</style>
