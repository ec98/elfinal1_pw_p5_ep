<template>
  <div class="pokemon">
    <img :src="imagen" :alt="texto" />
    <p>{{ texto }}</p>
  </div>
</template>
  
  <script>
export default {
  props: {
    imagen: String,
    texto: String
  }
};
</script>
  
  <style scoped>
.pokemon {
  display: grid;
  grid-template-rows: 100px 4px;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin: 10px;
}

.pokemon img {
  width: 100px; /* Ajusta el tamaño de la imagen según tus preferencias */
  height: auto;
  margin: 5px; /* Espaciado entre las imágenes */
}

.pokemon p {
  font-size: 14px;
  color: #333; /* Color del texto */
  margin: 0;
}
</style>
  