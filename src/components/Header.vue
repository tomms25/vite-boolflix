<script>
import { store } from '../store.js';
export default {
  data() {
    return {
      store,
    }
  }
}
</script>

<template>
  <header>
    <div class="container">
      <h1><a href="">BOOLFLIX</a></h1>

      <div class="search_bar">
        <!-- ricerca nell'api in base a cosa scrive l'utente -->
        <input type="search" placeholder="Scrivi qualcosa..." v-model="store.searchText">
        <button type="submit" @click.prevent="$emit('search')">
          Cerca
        </button>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
@use '../styles/partials/variables' as *;
header {
  background-color: black;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  margin-bottom: 10px;
  .container {
    justify-content: space-between;
    align-items: center;
    h1 {
      color: $accent;
    }
  }
}
</style>