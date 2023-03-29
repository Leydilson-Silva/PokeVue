<template>
  <div id="app">
    <nav class="navbar is-primary is-fixed-top">

      <div class="navbar-brand">
        <a class="navbar-item" href="https://leydilson-silva.github.io/PokeVue/">
          <img src="./assets/master.png" alt="Bulma: a modern CSS framework based on Flexbox">
          <h4 class="title is-3">PokeVue</h4>

        </a>
        <div class="navbar-burger" data-target="navbarExampleTransparentExample">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>

      

      <div class="navbar-end">
        <div class="navbar-item">
          <div class="field is-grouped">
            <p class="control">

              <input class="input is-rounded is-focused is-primary" type="text" name="Busca" placeholder="Buscar Pokemon"
                v-model="busca">
                
            </p>
            <p class="control">

              <button class="button is-primary" @click="buscar">Buscar</button>

            </p>
          </div>
        </div>
      </div>
    </nav>


    <div class="column container is-fullhd">
      <h4 class="title is-1 title-red">Pokedex</h4>
      <!-- <input class="input is-rounded is-half" type="text" name="Busca" placeholder="Buscar Pokemon" v-model="busca">
      <button class="button is-medium is-success buscarBtn" @click="buscar">Buscar</button> -->


      <div class="columns is-gapless is-multiline ">
        <div v-for="(poke) in filteredPokemons" :key="poke.url">
          <div class="column is-16">

            <Pokemon :number="pokemons.findIndex(_poke => _poke.name == poke.name) + 1 " :name="poke.name" :url="poke.url" />

          </div>
        </div>

      </div>

    </div>

    <footer class="footer is-fullwidth">
      <div class="content has-text-centered">
        <p>
          <strong>PokeVue</strong> by <a target="_blank" href="https://github.com/Leydilson-Silva">Leydilson Silva</a>.
          The source code is licensed
          <a target="_blank" href="http://opensource.org/licenses/mit-license.php">MIT</a>. The github hosted <a
            target="_blank" href="https://github.com/Leydilson-Silva/PokeVue">repository</a>.
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: '',
    };
  },
  created: function () {
    console.log("server started")

    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("pokemons captured");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;

    })
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == '' || this.busca == ' ') {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  computed: {
    // resultadoBusca: function(){
    //   if(this.busca == '' || this.busca == ' '){
    //     return ;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)  
    //   }
    // }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.buscarBtn {
  margin-top: 2%;
}
</style>