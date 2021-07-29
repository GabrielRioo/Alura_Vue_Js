<template>
  <div class="corpo">
    <h1 class="centralizado">{{ titulo }}</h1>

    <input class="filtro" type="search" placeholder="filtre por parte do titulo." v-on:input="filtro = $event.target.value"> 

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotos" v-bind:key="foto">
       <Meu-Painel :titulo="foto.titulo">
            <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo" />
       </Meu-Painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from './components/shared/painel/Painel.vue';
export default {
  components: {
    'Meu-Painel': Painel,
  },

  data() {
    return {
      titulo: "Alurapic",
      fotos: [],
      filtro:''
    };
  },

  created() {
    let promise = this.$http.get("http://localhost:3000/v1/fotos");
    promise
      .then(res => res.json())
      .then(
        fotos => (this.fotos = fotos),
        err => console.log(err)
      );
  }
};
</script>

<style>
.corpo {
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}

.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos-item {
  display: inline-block;
}

.imagem-responsiva {
  width: 100%;
  height: 70%;
}

.filtro {
  display: block;
  width: 100%;
  }

</style>
