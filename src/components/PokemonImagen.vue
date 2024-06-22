<template>
  <div class="pokemon-container">
    <img
      v-show="monstarPokemon"
      :src="imagenFuente"
      alt="No se puede cargar el pokemon"
    />

    <img
      v-show="!monstarPokemon"
      class="oculta-pokemon"
      :src="imagenFuente"
      alt="No se puede cargar el pokemon"
    />
  </div>
</template>

<script>
export default {
  props: {
    idPokemon: { type: Number, required: true, default: 1 },
    monstarPokemon: {
      required: true,
      type: Boolean,
    },
  },
  data() {
    return {
      monstar: false,
      ocultarOpciones: false
    };
  },

  computed: {
    imagenFuente() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.idPokemon}.svg`;
    },
  },
};
</script>

<style scoped>
.oculta-pokemon {
  filter: brightness(0);
}
img {
  height: 200px;
  width: 200px;
  position: absolute;
  right: 40%;
}

.pokemon-container {
  height: 200px;
}
</style>