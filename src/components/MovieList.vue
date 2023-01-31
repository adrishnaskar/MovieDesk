<template>
  <div class="movies-grid">
    <div v-for="movie in movies" :key="movie.id" class="movie">
      <router-link
        :to="{ name: 'Details', params: { id: movie.id } }"
        class="link"
      >
        <img :src="img_path + movie.poster_path" alt="Movie Poster" />

        <div class="rating">{{ movie.vote_average }}</div>

        <h3 class="title">{{ movie.title }}</h3>
        <div class="date">{{ movie.release_date }}</div>
        <div class="date">{{ movie.id }}</div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: ["movies"],
  setup(props) {
    const img_path = "https://image.tmdb.org/t/p/w500";
    return { img_path };
  },
};
</script>

<style>
.movies-grid{
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit,minmax(240px,1fr));
  margin: 2rem;
}

.movies-grid img {
  width: 100%;
  object-fit: cover;

}

.movie {
  position: relative;
  /* flex: 0 1 18%; */
  /* text-align: left; */
  /* padding: 10px; */
  margin: 10px;
  background: rgb(97, 1, 187);
}
.movie a {
  color: white;
  text-decoration: none;
}
.rating {
  background: black;
  border-radius: 50%;
  padding: 12px;
  display: inline;
  border: 5px solid rgb(0, 195, 255);
  position: absolute;
  top: auto;
  left: -1rem;
}
@media only screen and (min-width: 600px) {
  .movie h3 {
  margin: 1rem;
  max-width: 200px;
  text-align: center;
}
}


/* .rating{
  position: absolute;
  top: 200px;
  left: -10px;
  color: white;
 

} */

.movies-grid h1 {
  color: white;
  text-align: center;
}
.movie .date {
  padding-bottom: 20px;
}
</style>