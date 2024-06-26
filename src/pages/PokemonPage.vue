

<template>

  <div class="container">

    <h1 v-if="!pokemonCorrecto">Espere mienestras carga...</h1>
  <div  v-else>
    <h1>Selecciona el Pokemon Correcto</h1>
    <Score :intentos="intentos" :puntaje="puntaje"/>
  <PokemonImagen :idPokemon="pokemonCorrecto.id" :monstarPokemon="mostrar" />

  
  <div v-if="!ocultarOpciones">
    <PokemonOpciones :pokemons="arreglo" @seleccionPokemon="revisarRespuesta($event)" /> <!---Emitido hasta el padre-->
     
  </div>
<div v-else>
  <h2>Felicidades !!</h2>
</div>
<div v-if="pokemonErroneo"> <h1>Error! <br> Sigue intendando</h1></div>
  </div>

  </div>
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import Score from "../components/Score.vue";

//llamada al archivo externo que consume el API
import obtenerPokemonsFachada from "../clientes/clientePokemonAPI";

export default {
  components: {
    PokemonImagen,
    PokemonOpciones,
    Score
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
      this.intentos++;
      this.contador++;
      console.log(this.intentos)
      console.log(this.contador)
      console.log('Se emitio un evento desde el hijo')
      console.log(dato);
      
      if(dato.ident==this.pokemonCorrecto.id){
        this.mostrar=true;
        this.ocultarOpciones= true;
        this.pokemonErroneo=false;

       //SCORE LOGICA
       const puntajes=[0,10,8,5,3,2,1,0];
        if(this.intentos==this.contador){
          //console.log(puntajes[this.contador]);
          this.puntaje=puntajes[this.contador];}

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
      intentos:0,
      puntaje:0,
      contador:0,
      
    };
  },
  //no  necesitan el await ya que son de ciclo de vida
  mounted() {
    this.cargaInicial();
  },
};
</script>


<style>
h1, h2{
    color: yellow
}
</style>