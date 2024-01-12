<template>
  <div>
    <p>Puntaje: {{ puntaje }}</p>
    <p>Intento: {{ intento }}</p>

    <Pokemon :imagen="img1" texto="answer"></Pokemon>
    <Pokemon :imagen="img2" texto="answer"></Pokemon>
    <Pokemon :imagen="img3" texto="answer"></Pokemon>

    <button @click="consumirAPI()">JUGAR</button>

    <div v-if="intento >= 5 && puntaje <= 10">
      <p>Has utilizado tus {{ intento }} intentos</p>
      <p>El juego ha terminado, intentalo nuevamente</p>
      <button @click="reiniciar()">Nuevo Juego</button>
    </div>

    <div v-if="puntaje >= 10">
      <p>Puntaje: {{ puntaje }}</p>
      <p>Felicitaciones has ganado un premio de $10.000,00</p>
      <button @click="reiniciar()">Nuevo Juego</button>
    </div>
  </div>
</template>

<script>
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  components: {
    Pokemon
  },
  methods: {
    async getAPI() {
      const get = await fetch("https://yesno.wtf/api").then(p => p.json());
      this.answer = get.answer;
      // this.image = get.image;
      if(this.answer === 'no'){
        this.answer = "no";
      } else{
        this.answer = "yes";
      }
      if (this.intento === 0) {
        this.recibir = 0;
      }
      if (this.answer === "yes") {
        this.recibir++;
        if (this.recibir === 3) {
          this.puntaje += 5;
        } else if (this.recibir === 2) {
          this.puntaje += 2;
        } else if (this.recibir === 1) {
          this.puntaje += 1;
        }
      }

      this.img1 = get.image;
      this.img2 = get.image;
      this.img3 = get.image;
    },

    consumirAPI() {
      this.getAPI();
      this.puntajeIntento();
    },

    puntajeContar() {
      return this.puntaje++;
    },
    puntajeIntento() {
      return this.intento++;
    },
    reiniciar(){
      this.img1 = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg";
      this.img2 = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg";
      this.img3 = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg";
      this.puntaje = 0;
      this.intento = 0;
      this.recibir = 0;
    }
  },
  watch: {
    answer() {
      this.getAPI();
    }
  },
  data() {
    return {
      img1:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg",
      img2:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg",
      img3:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg",
      puntaje: 0,
      intento: 0,
      recibir: 0,
      answer: null
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
