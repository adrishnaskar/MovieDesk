<template>
<div class="main">
  <div class="hero">
    <!-- Search  -->
    <div class="search">
      <form @submit.prevent="handleSearch">
        <input type="text" placeholder="Search here..." v-model="search" />
        <button @click="handleSearch">Search</button>
      </form>
    </div>
  </div>

  <!-- Movies -->
  <div v-if="searchOn">
    <SearchedMovies />
  </div>
  <div v-else>
    <MovieList :movies="movies" />
  </div>

  </div>
</template>

<script>
// imports-------------------

import { ref } from "@vue/reactivity";
import MovieList from "../components/MovieList.vue";
import Details from "./Details.vue";
import SearchedMovies from "../components/SearchedMovies.vue";
import { onMounted } from "@vue/runtime-core";
import MOVIE_API from '../../api_key.js'

export default {
  components: { MovieList, SearchedMovies, Details },

  setup() {
    // const MY_API_KEY = process.env.API_KEY
    // console.log(process.env.API_KEY)
    const searchOn = ref(false);
    const api_url = ref(
      `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${MOVIE_API}&page=1`
    );
    const search_api = ref(
      `https://api.themoviedb.org/3/search/movie?api_key=${MOVIE_API}&query=`
    );
    const movies = ref([]);
    const search = ref(null);
    // const date = ref(movies.release_date.toISOString())

    // getting the data ------------------------------
    onMounted(() => {
      
      getMovies(api_url.value);

      // fetch(api_url.value)
      //   .then((res) => res.json())
      //   .then((data) => {
      //     console.log(data);
      //     setMovies(data.results);
      //     movies.value =data.results
      //   });
    });
    const getMovies = async (url) => {
        try {
          const res = await fetch(url);
          const data = await res.json();
          // console.log(data)
          movies.value = data.results;
          // console.log(movies);
          setMovies(data.results);
        } catch (err) {
          console.log(err.message);
        }
      };

    function setMovies(movies) {
      // movies.value = movies;
      movies.forEach((movie) => {
        const { title, id, poster_path, vote_average, overview, release_date } =
          movie;
      });
    }

      async function  handleSearch() {
      // const search_term = search.value;
      if (search.value !=="") {
       
        await getMovies(search_api.value + search.value)
        search.value = ''
        
      } else {
        console.log('cannot find the movie')
      }
    }

    return { searchOn, movies, handleSearch, search };
  },
};
</script>

<style>
body {
  background: #121212;
}

/* hero style */
.hero {
  margin: 3rem auto 3rem auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  color: white;
}

/* hero fonts */
.hero h1 {
  font-size: 2.5rem;
}
.hero p {
  font-size: 1.2rem;
}

/* search styles */
.search button {
  background: rgb(97, 1, 187);
  border: none;
  color: white;
  padding: 16px 24px;
  font-style: bold;
  cursor: pointer;
}
.search input {
  padding: 12px 500px 12px 12px;
  font-size: 16px;
  border: 2px solid rgb(131, 131, 131);
}

/* for mobile devices */
@media (max-width: 800px) {
  .search {
    display: flex;
  }
  .search input {
    padding: 12px 60px 12px 8px;
  }
}
</style>