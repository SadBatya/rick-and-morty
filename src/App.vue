<script setup>
import CardPerson from './components/CardPerson.vue';
import FilterPanel from './components/FilterPanel.vue';
</script>

<template>
  <FilterPanel />
  <div class="navigation_panel">
    <input type="text" />
    <div>
      <select name="status" v-model="selectedStatus">
        <option value=" ">All</option>
        <option value="Alive">Alive</option>
        <option value="Dead">Died</option>
      </select>
    </div>
    
    <button @click="sortByStatus(selectedStatus)">Применить</button>
  </div>

  <div class="cards">
    <CardPerson
      v-for="(person, index) in characters"
      :key="index"
      :name="person.name"
      seen="The Ricklantis Mixup"
      location="Citadel of Ricks"
      :status="person.status"
      :img="person.image"
    />
  </div>
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
      sortedCharacter: [],
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
    sortByStatus(status) {
      axios
        .get(`https://rickandmortyapi.com/api/character/?status=${status}`)
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
.navigation_panel {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
  padding: 1rem;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center;
}

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
