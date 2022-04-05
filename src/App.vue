<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <ul class="navbar-nav">
        <li class="nav-item m-2">
          <a href="" class="nav-link">asd</a>
        </li>
        <li class="nav-item m-2">
          <a href="" class="nav-link">asd</a>
        </li>
      </ul>
  </nav>
  
  <div class="row m-1" id="tablazat">
    <div v-for="vizsgaidopont in vizsgaidopontok" :key="vizsgaidopont.id" class="col-xl-4 col-md-6 col-12">
      <div class="m-2 card p-3">
        <h2>{{vizsgaidopont.targy}}</h2>
        <h4>{{vizsgaidopont.tipus}}</h4>
        <p>{{vizsgaidopont.kezdes}}</p>
      </div>
    </div>
  </div>
  <div>

  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      vizsgaidopontok: [],
    }
  },
  methods: {
    async feltoltes() {
      await axios
        .get('http://127.0.0.1:8000/api/vizsgaidopontok')
        .then(response => this.vizsgaidopontok = response.data)
    }
  },
  mounted() {
    this.feltoltes()
  }
}
</script>

<style>
</style>
