<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <edit-table :apiUrl="apiUrl" :language="selectedLanguage"></edit-table>
  </div>
</template>

<script>
import editTable from './components/ui-editable-table.vue';
import axios from 'axios';

const baseUrl = "http://localhost:3000/api/language";

export default {
  name: 'app',
  components: {
    'edit-table': editTable
  },
  created () {
    // this.apiUrl = baseUrl + this.selectedLanguage;
  },
  data () {
    return {
      apiUrl: baseUrl,
      msg: 'Welcome to Your Vue.js App',
      selectedLanguage: "ga"
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
