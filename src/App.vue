<script>
import axios from 'axios';
import MoviesCardList from './components/MoviesCardList.vue'
import Header from './components/Header.vue';
import { store } from './store.js';
export default {
  components: {
    MoviesCardList,
    Header,
  },
  data() {
    return {
      store,
    }
  },
  methods: {
    getMovies() {
      let myUrl = store.moviesAPI;
      // se l'utente scrive il nome di un film, myUrl viene sostituito dalla query del film cercato e simili
      if (store.searchText !== '') {
        myUrl = `https://api.themoviedb.org/3/search/movie?api_key=6fd82c7e095558dcca8a44519f3dc58a&query=${store.searchText}`
      }
      // per connettersi all api
      axios
        .get(myUrl)
        .then(res => {
          store.moviesList = res.data.results
        }
        )
    },
    getTv() {
      let myUrl = store.tvAPI;
      if (store.searchText !== '') {
        myUrl = `https://api.themoviedb.org/3/search/tv?api_key=6fd82c7e095558dcca8a44519f3dc58a&query=${store.searchText}`
      }
      axios
        .get(myUrl)
        .then(res => {
          store.tvList = res.data.results
        }
        )
    },
    searchBoth() {
      this.getMovies()
      this.getTv()
    },
  },
  mounted() {
    this.searchBoth()
  }
}
</script>

<template>
  <Header @search="searchBoth" />
  <main>
    <MoviesCardList />
  </main>
</template>

<style lang="scss">
@use './styles/general.scss' as *;
</style>