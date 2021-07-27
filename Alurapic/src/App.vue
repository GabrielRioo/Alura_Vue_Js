<template>
  <div>
    <h1>{{ titulo }}</h1>

    <ul>
      <li v-for="foto of fotos" v-bind:key="foto">
        <img v-bind:src="foto.url" v-bind:alt="foto.titulo" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: "Alurapic",
      fotos: [
        {
          url: "http://placehold.it/300x300",
          titulo: "cachorro"
        },
        {
          url: "http://placehold.it/300x300",
          titulo: "Cachorrão"
        }
      ]
    };
  }
};
</script>

<style></style>
