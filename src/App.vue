<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <ul class="navbar-nav">
        <li class="nav-item m-2">
          <a href="#tablazat" class="nav-link">Táblázat</a>
        </li>
        <li class="nav-item m-2">
          <a href="#form" class="nav-link">Form</a>
        </li>
      </ul>
  </nav>
  
  <div class="row m-1" id="tablazat">
    <div v-for="vizsgaidopont in vizsgaidopontok" :key="vizsgaidopont.id" class="col-xl-4 col-md-6 col-12">
      <div class="m-2 card p-3">
        <h2>{{vizsgaidopont.targy}}</h2>
        <h4>{{vizsgaidopont.tipus}}</h4>
        <p>{{vizsgaidopont.kezdes}}</p>
        <img :src="kep(vizsgaidopont.tipus)" class="kep">
      </div>
    </div>
  </div>
  <div id="form">
    <input type="text" v-model="vizsgaidopont.targy" placeholder="Tárgy" class="w-50 btn border"><br>
    <input type="text" v-model="vizsgaidopont.tipus" placeholder="Tipus" class="w-50 btn border"><br>
    <input type="datetime-local" v-model="vizsgaidopont.kezdes" class="w-50 btn border"><br>
    <button class="btn btn-primary w-50" @click="hozzaadas">Hozzáadás</button>
  </div>
</template>

<script>

import axios from 'axios'
import { error } from 'console'

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      vizsgaidopontok: [],
      vizsgaidopont: {
        targy: '',
        tipus: '',
        kezdes: null
      }
    }
  },
  methods: {
    async listazas() {
      await axios
        .get('http://127.0.0.1:8000/api/vizsgaidopontok')
        .then(response => this.vizsgaidopontok = response.data)
        .catch(error => console.log(error))
    },
    async hozzaadas() {
      console.log(this.vizsgaidopont)
      await axios
        .post('http://127.0.0.1:8000/api/vizsgaidopontok', this.vizsgaidopont)
        .then(response => this.vizsgaidopontok = response.data)
        .catch(error => console.log(error))
      this.listazas()
      this.vizsgaidopont = {
        targy: '',
        tipus: '',
        kezdes: null
      }
    },
    kep(tipus) {
      let kep = null
      if(tipus == 'erettsegi') {
        kep = require('./assets/erettsegi.jpg')
      }
      else if(tipus == 'szakmai') {
        kep = require('./assets/szakmai.jpeg')
      }
      return kep
    }
  },
  mounted() {
    this.listazas()
  }
}
</script>

<style>
.kep {
  width: 300px;
  height: 300px;
  margin: auto;
}
#form {
  text-align: center;
}
input {
  margin: 10px auto !important;
  cursor: text !important;
}
button {
  margin: 10px auto !important;
}
</style>
