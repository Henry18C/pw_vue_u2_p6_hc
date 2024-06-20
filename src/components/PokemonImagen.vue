<template>
 
<div class="pokemon-container">
    <img v-show="monstar"
    src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/6.svg"
    alt="No se puede cargar el pokemon"
  />

  <img v-show="!monstar"
    class="oculta-pokemon"
    src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/6.svg"
    alt="No se puede cargar el pokemon"
  />

</div>

</template>

<script>
export default {

    data() {
    return {
      
      monstar: false,
    
    }}};
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


.pokemon-container{
    height: 200px;
}
</style>