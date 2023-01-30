<script>
import axios from 'axios';
import { api } from './data'
import { store } from './data/store'
import SearchBar from './components/Generics/SearchBar.vue';
import AppMain from './components/AppMain.vue';
import ProductionCard from './components/Generics/ProductionCard.vue';

// import appHeader from './components/AppHeader.vue'
export default {
  name: 'Boolflix',
  components: { SearchBar, AppMain, ProductionCard },
  data() {
    return {
      store,
      titleFilter: ''
    }
  },
  computed: {
    axiosConfig() {
      const { key, language } = api;
      return {
        params: {
          language: language,
          api_key: key,
          query: this.titleFilter
        }
      }

    }
  },
  methods: {
    updateTitleFilter(term) {
      this.titleFilter = term
    },
    searchProduction() {
      if (!this.titleFilter) {
        store.movies = [];
        store.series = [];
        return;
      }
      this.fetchApi('search/movie', 'movies');
      this.fetchApi('search/tv', 'series');
    },
    fetchApi(endpoint, collection) {
      axios.get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
        .then(res => {
          store[collection] = res.data.results;
        }).catch(err => { console.error(err) })
    }
  }

}
</script>
<template>
  <header>
    <nav>
      <h2>BOOFLIX</h2>
      <search-bar placeholder="Cerca un film" @term-change="updateTitleFilter"
        @form-submit="searchProduction"></search-bar>
    </nav>
  </header>

  <app-main></app-main>

</template>
<style  lang="scss">
@use './assets/sass/style.scss';
</style>