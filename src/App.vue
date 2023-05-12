<script>
import ref from 'vue';
import Card from './components/Card.vue';

export default {
  setup() {
    const search_query = ref("");

    return {
      Card,
      search_query
    }
  }
}
</script>

<template>
  <div class="app">
    <header>
      <h1>The<strong>Anime</strong>Tracker</h1>
      <form class="search-box">
        <input type="search" class="search-field" placeholder="Rechercher un anime..." />
      </form>
    </header>
    <main>
      <div class="cards">
        <Card />
      </div>
    </main>
  </div>
</template>
