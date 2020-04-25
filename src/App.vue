<template>
<div id="app">
  <h1>WhichPort</h1>
  <input v-model="query" id="main_input" type="text" placeholder="Type an app name…" autofocus />
  <ul class="result-list">
    <li class="result-item" v-for="result of searchResults" :key="result.name">
      <h2 class="app-title">{{result.name}}</h2>
      <h3 class="app-port">{{result.port}}</h3>
      <a class="app-link" v-bind:href="URL_BASE + result.port">Open</a>
    </li>
  </ul>
</div>
</template>

<script>
import DATA from './DATA.js';
const URL_BASE = 'http://localhost:';

export default {
  name: 'App',
  data() {
    return {
      query: '',
      URL_BASE,
    };
  },
  computed: {
    searchResults() {
      if (this.query.length === 0) return [];
      return DATA.filter(x => x.name.toLowerCase().startsWith(this.query.toLowerCase()));
    }
  },
}
</script>

<style>
#main_input {
  border: 1px solid black;
  border-radius: 5px;
  /* height: 4em; */
  font-size: 4em;
  width: 80%;
}

.result-list {
  list-style-type: none;
  width: 80%;
  font-size: 3em;
  padding: 0.5em;
  box-shadow: 5px 6px 10px 4px #9e9e9e;
}

.result-item:not(:last-child) {
  border-bottom: 1px solid #9e9e9e;
}

.result-item .app-title {
  display: inline;
  margin: 0;
}

.result-item .app-port {
  display: inline;
  color: #aaaaaa;
  margin: 0;
  margin-left: 2em;
  /* text-align: right; */
}

.result-item .app-link {
  float: right;
}
</style>
