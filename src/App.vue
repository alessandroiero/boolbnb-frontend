<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  // metodo data per fare chiamate api axios
  data() {
    return {
      apiBaseUrl: 'http://127.0.0.1:8000/api',
      apiUrls: {
        projects: '/projects'
      },
      projects: []
    }
  },
  // componenti
  components: {
    AppHeader,
    AppMain,
    AppFooter
  },
  // dentro methods inseriamo le funzioni e i vari metodi
  methods: {
    getProjects() {
      axios.get(this.apiBaseUrl + this.apiUrls.projects)
        //chiamata asyncrona
        .then((response) => {
          this.projects = response.data.results;
        })
        // in caso di errore
        .catch((error) => {
          console.log(error);
        })
    }
  },
  // lifecycle created - chiamata api
  created() {
    this.getProjects();
  }

}
</script>

<template>
  <AppHeader />
  <AppMain :data="posts" />
  <AppFooter />
</template>


<style lang="scss">
//versione 1 - inclusione via app.vue
// @use './assets/scss/main.scss' as *;
</style>
