<script>
import { ref } from 'vue';
import Card from './components/Card.vue';

export default {
  components: {
    Card
  },
  setup() {
    const search_query = ref("");
    const animelist = ref([]);

    const handleSearch = async () => {
      const res = await fetch(`https://api.jikan.moe/v4/anime?q=${search_query.value}`);
      const resData = await res.json();
      animelist.value = resData.data;

      search_query.value = "";
    };

    return {
      search_query,
      animelist,
      handleSearch
    };
  }
}
</script>

<template>
  <div class="app">
    <header>
      <h1>The<strong>Anime</strong>Tracker</h1>
      <form class="search-box" @submit.prevent="handleSearch">
        <input type="search" class="search-field" placeholder="Rechercher un anime..." required v-model="search_query" />
      </form>
    </header>
    <main>
      <div class="cards" v-if="animelist.length > 0">
        <Card v-for="anime in animelist" :key="anime.mal_id" :anime="anime" />
      </div>
      <div class="no-results" v-else>
        <h3>Désolé, il n'y a pas de résultats</h3>
      </div>
    </main>
  </div>
</template>
