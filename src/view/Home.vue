<script setup>
import { ref, onBeforeMount, defineAsyncComponent } from "vue"
import MovieList from "../components/MovieList.vue";
import SearchInput from '../components/SearchInput.vue';
const movies = ref([])
const bannerMovie = ref(null)
const text = ref('')

const AsyncBanner = defineAsyncComponent(() => {
  return import("../components/Banner.vue")
})

const getMovies = async () => {
  movies.value = await fetch("https://api.themoviedb.org/3/movie/popular?api_key=4e44d9029b1270a757cddc766a1bcb63&language=en-US")
  .then(res => res.json())
  .then(res => res.results)
}

function getRandomInt (min, max)  {
  return Math.floor(Math.random() * (max - min) + min)
}     
const SearchMovies = (searchText) => {
  text.value = searchText;
  if (text.value != "") {
    fetch(
      `https://api.themoviedb.org/3/search/movie?api_key=4e44d9029b1270a757cddc766a1bcb63&query=${text.value}&include_adult=false&language=en-US`
    )
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        movies.value = data.results;
        text.value = "";
      });
  }
};
onBeforeMount(async() => {
  await getMovies() 
  bannerMovie.value = movies.value[getRandomInt(0, movies.value.length - 1)]
})

</script>

<template>
    <AsyncBanner 
    :banner="bannerMovie"
    v-if="bannerMovie"
    />
  <SearchInput :movies="movies" @sendText="SearchMovies"/>
    <MovieList 
    :movies="movies"
    />
</template>