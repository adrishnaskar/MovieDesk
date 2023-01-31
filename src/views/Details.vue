<template>
  <div class="parent">
    
    <img class="img_post" :src="img_path + poster_path" alt="" />
    <div class="avg"><b>Rating: </b>{{ vote_average}}</div>

    <h1 class="titl">{{ title }}</h1>
    <p class="rls"><b>Date Released: </b>{{ release_date }}</p>
    <div class="des"><b>Summary: </b>
    <p >{{ overview }}</p></div>
    
    
    <!-- 
    get single movie using the param id

   -->
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { useRoute } from "vue-router";
import { onMounted } from "@vue/runtime-core";
export default {
  setup() {
    const route = useRoute();
    const movie = ref();
    const title = ref("");
    const poster_path = ref("");
    const img_path = ref("https://image.tmdb.org/t/p/w500");
    const overview = ref("");
    const vote_average = ref("");
    const release_date = ref(null);

    onMounted(() => {
      const getMovie = async (id) => {
        try {
          const res = await fetch(
            "https://api.themoviedb.org/3/movie/" +
              id +
              "?api_key=2a8518c6ae8d6c8a2d0b6f6d40bee70f"
          );
          const data = await res.json();

          movie.value = data;
          title.value = data.title;
          poster_path.value = data.poster_path;

          overview.value = data.overview;
          vote_average.value = data.vote_average;
          release_date.value = data.release_date;
          //   const { title, poster_path, vote_average, overview, release_date } =
          //     data;

          //   title.value = data.title;
          // console.log(movie);
          // console.log(data);
        } catch (err) {
          console.log(err.message);
        }
      };
      getMovie(route.params.id);

      // fetch(api_url.value)
      //   .then((res) => res.json())
      //   .then((data) => {
      //     console.log(data);
      //     setMovies(data.results);
      //     movies.value =data.results
      //   });
    });
    return {
      movie,
      title,
      poster_path,
      overview,
      vote_average,
      release_date,
      img_path,
    };
  },
};
</script>

<style>
@media (min-width: 800px) {
  .parent {
  color: #ffffff;
  text-align: left;
  display: grid;
  grid-template-areas: 
  'img titl'
 'img rls'
 'img rate'
 'img des'
 
  ;


  grid-template-columns: auto-fit 70%;
  /* grid-template-rows: 0.2fr 1.5fr 1.5fr 1.5fr; */
  grid-template-rows: repeat(2fr 1fr 1fr 3fr);
  grid-column-gap: 2rem;
  /* grid-row-gap: 10px; */
  margin: 4rem;
}

.img_post{
  grid-area: img;
max-width: 300px; 
 object-fit: cover;
}
.avg{
  grid-area: rate;
}
.titl{
  grid-area: titl;
}
.rls{
  grid-area: rls;
}
.des{
  grid-area: des;
  font-size: 1.4rem;
}
}


/* mobile */
@media (max-width: 800px) {
.parent {
  color: #ffffff;
  margin: 2rem;}

.img_post{
  grid-area: img;
  max-width: 300px; 
  object-fit: cover;
}
.des{
  font-size: 1.2rem;
  
}}
</style>