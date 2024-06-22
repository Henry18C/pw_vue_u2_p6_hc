

<template>

  <h1 v-if="!pokemonCorrecto">Espere mienestras carga...</h1>
  <div  v-else>
    <h1>Selecciona el Pokemon Correcto</h1>
  <PokemonImagen :idPokemon="pokemonCorrecto.id" :monstarPokemon="mostrar" />

  <div v-if="pokemonErroneo"> <h1>Error Sigue intendando</h1></div>
  <div v-if="!ocultarOpciones">
    <PokemonOpciones :pokemons="arreglo" @seleccionPokemon="revisarRespuesta($event)" /> <!---Emitido hasta el padre-->
     
  </div>
<div v-else>
  <div>Felicidades !!</div>
</div>

  </div>
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
      const vectorInicial = await obtenerPokemonsFachada(7);
      this.arreglo = vectorInicial;
      const indice = Math.floor(Math.random() * 7);

      this.pokemonCorrecto = this.arreglo[indice];
    },
    revisarRespuesta(dato){
      console.log('Se emitio un evento desde el hijo')
      console.log(dato);
      
      if(dato.ident==this.pokemonCorrecto.id){
        this.mostrar=true;
        this.ocultarOpciones= true;
        this.pokemonErroneo=false;

      }else{
        console.log("ERROR...")
        this.pokemonErroneo=true;

      }
    },
  },
  data() {
    return {
      arreglo: [],
      pokemonCorrecto: null,
      mostrar: false,
      ocultarOpciones:false,
      pokemonErroneo:false,
      
    };
  },
  //no  necesitan el await ya que son de ciclo de vida
  mounted() {
    this.cargaInicial();
  },
};
</script>


<style>
</style>