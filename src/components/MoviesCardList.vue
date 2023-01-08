<script >
import { store } from '../store.js';
export default {
  data() {
    return {
      active: {},
      store,
    }
  },
  methods: {
    // metodo per visualizzare bandiere in base alla lingua
    displayLanguage(language) {
      if (language === 'en') {
        return '<img class="flag" src="https://flagcdn.com/16x12/gb.png" alt="uk-flag" />';
      }
      else if (language === 'it') {
        return '<img class="flag" src="https://flagcdn.com/16x12/it.png" alt="it-flag" />';
      }
      else {
        return language;
      }
    },
    rating(voteAverage) {
      let vote = Math.round(voteAverage / 2);
      return vote;
    }
  }
}
</script>

<template>
  <div class="container">
    <!-- cicla nell'array dei film e quando il mouse va sulla specifica card (con id) del film, appaiono le info-->
    <div class="card" v-for="movie in store.moviesList" :key="movie.id" @mouseover="active[movie.id] = true"
      @mouseout="active[movie.id] = false">
      <!-- immagine del film -->
      <img :src="movie.poster_path ? `https://image.tmdb.org/t/p/w185${movie.poster_path}` : 'img/image-not-found.jpg'"
        :alt="movie.title">

      <!-- Parte che compare on hover sulla card con tutti i dettagli -->
      <div class="details" v-show="active[movie.id]">
        <!-- titolo film -->
        <h4>Titolo: {{ movie.title }}</h4>
        <h4 v-if="movie.title != movie.original_title">Titolo originale: {{ movie.original_title }}</h4>
        <!-- condizione per bandiera o stringa lingua -->
        <h5 :innerHTML="displayLanguage(movie.original_language)">
        </h5>
        <!-- votazione film -->
        <div class="rating">
          Voto:
          <!-- stampa stelle in base alla votazione -->
          <span v-for="star in rating(movie.vote_average)">&#9733;</span>
          <!-- stampa le rimanenti stelle vuote, facendo la differenza tra un intervallo di 5 numeri meno il voto arrotondato del metodo-->
          <span v-for="star in 5 - rating(movie.vote_average)">&#9734;</span>
        </div>

        <h6>{{ movie.overview }}</h6>
      </div>
    </div>

    <!--cicla nell' array delle serie tv e quando il mouse va sulla specifica card (con id) della serie, appaiono le info-->
    <div class="card" v-for="tv in store.tvList" :key="tv.id" @mouseover="active[tv.id] = true"
      @mouseout="active[tv.id] = false">

      <!-- immagine -->
      <img :src="tv.poster_path ? `https://image.tmdb.org/t/p/w185${tv.poster_path}` : 'img/image-not-found.jpg'"
        :alt="tv.name">

      <!-- Parte che compare on hover sulla card con tutti i dettagli -->
      <div class="details" v-show="active[tv.id]">
        <!-- titolo -->
        <h4>Titolo: {{ tv.name }}</h4>

        <!-- mostra titolo originale se diverso da titolo -->
        <h4 v-if="tv.name != tv.original_name">Titolo originale: {{ tv.original_name }}</h4>

        <!-- condizione per bandiera o stringa lingua -->
        <h5 :innerHTML="displayLanguage(tv.original_language)">
        </h5>

        <!-- votazione serie -->
        <div class="rating">
          Voto:
          <span v-for="star in rating(tv.vote_average)">&#9733;</span>
          <span v-for="star in 5 - rating(tv.vote_average)">&#9734;</span>
        </div>

        <h6>{{ tv.overview }}</h6>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use '../styles/partials/variables' as *;
.container {
  margin-top: 50px;
  .card {
    cursor: pointer;
    position: relative;
    color: $text;
    width: 185px;
    img {
      width: 185px;
      height: 278px;
      object-fit: cover;
    }
    .details {
      padding: 10px;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba($color: #000000, $alpha: 0.7);
      overflow-y: auto;
      h4,
      .rating {
        font-size: 0.8rem;
        margin-bottom: 10px;
      }
      span {
        color: yellow;
      }
      h6 {
        font-size: 0.75rem;
        font-weight: 100;
      }
    }
  }
}
</style>