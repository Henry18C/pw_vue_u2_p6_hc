<template>
  <div class="opciones-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('seleccionPokemon',{ident:pokemon.id,nomb:pokemon.nombre})" 
      > <!---Emite al padre. Como primer argumeto el nombre de la emision y como segundo el dato que deseo emitir       -->
        {{ pokemon.nombre }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
ul {
  list-style-type: none;
}

li {
  border: solid 1px yellow;
  border-radius: 5px;
  margin-bottom: 5px;
  width: 250px;
  background: white;
  cursor: pointer;
}

li:hover {
  background: rgba(0, 0, 0, 0.05);
}

.opciones-container {
  display: flex;
  justify-content: center;
}
</style>