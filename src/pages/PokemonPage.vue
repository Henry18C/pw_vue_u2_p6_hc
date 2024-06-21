

<template>
  <h1>Selecciona el Pokemon Correcto</h1>

  <PokemonImagen :idPokemon="6" :monstarPokemon="false" />
  <PokemonOpciones :pokemons="5" />
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";

//llamada al archivo externo que consume el API
import obtenerPokemonsFachada from "../clientes/clientePokemonAPI";

export default {
  components: {
    PokemonImagen,
    PokemonOpciones,
  },

  methods: {
    //llamada al archivo externo que consume el API
    async cargaInicial() {
      const vectorInicial = await obtenerPokemonsFachada(4);
      this.arreglo=vectorInicial;
    },
  },
  data() {
    return {
      arreglo: [],
    };
    
  },
  //no  necesitan el await ya que son de ciclo de vida
  mounted(){
    this.cargaInicial();
  }

};
</script>


<style>
</style>