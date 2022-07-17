<template>
  <h3>Pokemon options</h3>

  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selectedPkemon', pokemon.id)"
      >
        {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  emits: ["selectedPkemon"],
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.options-container {
  display: flex;
  justify-content: center;
}

/* Pokemon Options */
ul {
  list-style-type: none;
  padding-inline-start: 0;
}
li {
  background-color: white;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
  width: 250px;
}

li:hover {
  background-color: rgba(0, 0, 0, 0.05);
}
</style>