<template>
  <div class="container cont">
    <div class="row">
      <div class="col-md-12">
        <label for="">Nombre:</label>
        <input type="text" placeholder="Nombre pokemon" v-model="namePokemon" />
        <button @click="searchPokemon">Buscar</button>
        <div v-for="(pokemon, index) in pokemones" :key="index">
          <p>{{ pokemon.name }}</p>
        </div>
        <img :src="showImg" alt="" />
        <h2>Movimientos</h2>
        <p v-for="(item, index) in showMove" :key="index">
          {{ item.move.name }}
        </p>
        <h2>Habilidades</h2>
        <p v-for="(item, index) in showAbilities" :key="index">
          {{ item.ability.name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pokemones",
  props: {},
  data() {
    return {
      namePokemon: "pikachu",
      pokemones: null,
    };
  },
  created() {
    this.getPokemonData();
  },
  methods: {
    getPokemonData() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.namePokemon}`)
        .then((response) => response.json())
        .then((datosPokemon) => {
          this.pokemones = datosPokemon;
          console.log(datosPokemon);
        });
    },
    searchPokemon() {
      //e.preventdefault();
      this.getPokemonData(this.namePokemon);
      console.log("buscar", this.namePokemon);
    },
  },
  computed: {
    showImg() {
      return this.pokemones.sprites.front_default;
    },
    showAbilities() {
      return this.pokemones.abilities;
    },
    showMove() {
      return this.pokemones.moves;
    },
  },
};
</script>

<style scoped>
</style>