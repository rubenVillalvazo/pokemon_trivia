<template>
  <div class="pokemonImage pokemon-container">
    <img
      v-if="!showPokemon"
      class="hiddenPokemon"
      :src="imgSrc"
      alt="Pokemon"
    />
    <img v-else class="fade-in" :src="imgSrc" alt="Pokemon" />
  </div>
</template>

<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true,
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  data() {
    return {
      id: this.pokemonId,
    };
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.id}.svg`;
    },
  },
};
</script>

<style lang="scss" scoped>
/* Pokemon Picture */
.pokemon-container {
  display: flex;
  justify-content: center;
  height: 200px;
  width: 100%;
}
img {
  height: 200px;
  position: absolute;
  margin: auto;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}
.hiddenPokemon {
  filter: brightness(0);
}
</style>