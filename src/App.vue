<script setup>
import CardPerson from './components/CardPerson.vue';
import FilterPanel from './components/FilterPanel.vue';
</script>

<template>
  <FilterPanel />

  <CardPerson
    v-for="(person, index) in characters"
    :key="index"
    :name="person.name"
    seen="The Ricklantis Mixup"
    location="Citadel of Ricks"
    :status="person.status"
    :img="person.image"
  />
  <div class="pagination_panel">
    <button
      :disabled="page === 1"
      @click="prevPage"
      class="pagination_button"
    >
      &#128072;
    </button>
    <h1>{{ page }} из {{ totalPages }}</h1>
    <button
      :disabled="page === totalPages"
      @click="nextPage"
      class="pagination_button"
    >
      &#128073;
    </button>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      characters: [],
      page: 1,
      totalPages: null,
    };
  },
  created() {
    this.fetchCharacters();
  },
  methods: {
    fetchCharacters() {
      axios
        .get(`https://rickandmortyapi.com/api/character?page=${this.page}`)
        .then((res) => {
          this.characters = res.data.results;
          this.totalPages = res.data.info.pages;
        })
        .catch((e) => {
          console.error('Ошибка при получении персонажей:', e);
        });
    },
    nextPage() {
      if (this.page < this.totalPages) {
        console.log('click');
        this.page++;
        this.fetchCharacters();
      }
    },
    prevPage() {
      if (this.page > 1) {
        this.page--;
        this.fetchCharacters();
      }
    },
  },
};
</script>
<style scoped>
.pagination_panel {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.pagination_button {
  width: 5rem;
  height: 3rem;
}
</style>
