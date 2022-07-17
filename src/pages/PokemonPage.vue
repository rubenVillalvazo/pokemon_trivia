<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else>
    <h1>¿Quien es este pokémon?</h1>
    <PokemonData :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions
      :pokemons="pokemonsCollection"
      @selectedPkemon="checkAnswer"
    />

    <template v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame">Nuevo juego</button>
    </template>
  </div>
</template>

<script>
/* Vue components */
import PokemonData from "@/components/PokemonData";
import PokemonOptions from "@/components/PokemonOptions";

/* Js components */
import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  components: {
    PokemonData,
    PokemonOptions,
  },
  data() {
    return {
      pokemonsCollection: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonCollection() {
      this.pokemonsCollection = await getPokemonOptions();
      const randomInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonsCollection[randomInt];
    },
    checkAnswer(selectedPokemon) {
      this.showPokemon = true;
      this.showAnswer = true;
      if (selectedPokemon === this.pokemon.id) {
        this.message = `A huevo...! Es ${this.pokemon.name}!!!`;
      } else {
        this.message = `No mames...! Te hace falta mas pokemon, es ${this.pokemon.name}`;
      }
    },
    newGame() {
      this.pokemonsCollection = [];
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemon = null;
      this.mixPokemonCollection();
    },
  },
  mounted() {
    this.mixPokemonCollection();
  },
};
</script>

<style>
</style>