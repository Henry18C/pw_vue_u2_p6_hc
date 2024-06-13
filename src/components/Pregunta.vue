<template>
  <img v-if="img!=null"
    :src="img"
    alt="None"
  />
  <div class="oscuro"></div>
  <div class="pregunta-container">
    <input v-model="pregunta" type="text" placeholder="Hazme una pregunta" />

    <p>Recuera teminar la pregunta con el signo de interrogacion (?)</p>

    <div class="respuesta">
      <h2>{{ pregunta }}</h2>
      <h1>{{ respuesta }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pregunta: null,
      respuesta: null,
      img: null
    };
  },
  watch: {
    pregunta(value, oldvalue) {
      console.log({ value, oldvalue });
      if (!value.includes("?")) {
        return; //salgase del observador
      }

      //consumir el API para obtener la respuesta

      console.log("Se hizo la pregunta");
      this.obtenerRespuesta();

    },
  },
  methods: {
     async obtenerRespuesta() {
      //fetch("URl del API").then(respuesta)
      //el await hacer que espere la respuesta
      this.respuesta= "Pensando..."
      const data= await fetch("https://yesno.wtf/api").then((resp) => resp.json());
      const {answer, forced, image}= data;
      console.log(answer);
      this.respuesta= answer,
      this.img= image;
      return data;
    },
  },

 async prueba(){
  const data2 = await this.obtenerRespuesta();
 }

};
</script>

<style>
img,
.oscuro {
  max-height: 100%;
  height: 1000vh;
  max-width: 100%;
  width: 100vw;
  position: fixed;
  top: 0px;
  left: 0px;
}
.oscuro {
  background: rgb(0, 0, 0, 0.4);
  /*0.0 es full trasparente 1.0 full opaco */
}

.pregunta-container {
  position: relative; /* solucionamos el punto de que estab atras, independientemente de los elementos que este se coloca por encima */
}

input {
  margin-top: 70px;
  width: 260px;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
}

input:focus {
  outline: none;
}

p,
h1,
h2 {
  color: white;
}

p {
  font-size: 20px;
  margin-top: 0px;
}

.respuesta {
  margin-top: 90px;
}
</style>