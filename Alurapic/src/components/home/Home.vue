<template>
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>

    <input
      class="filtro"
      type="search"
      placeholder="filtre por parte do titulo."
      @input="filtro = $event.target.value"
    />

    <ul class="lista-fotos">
      <li
        class="lista-fotos-item"
        v-for="foto of fotosComFiltro"
        v-bind:key="foto"
      >
        <Meu-Painel :titulo="foto.titulo">
          <Imagem-Responsiva :url="foto.url" :titulo="foto.titulo" />
          <Meu-Botao
            tipo="button"
            rotulo="REMOVER"
            @botaoAtivado="remove(foto)"
            :confirmacao="true"
            estilo="perigo"
          />
          <!-- <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo" /> -->
        </Meu-Painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import ImagemResponsiva from "../shared/imagem-responsiva/ImagemResponsiva.vue";
import Botao from "../shared/botao/Botao.vue";

export default {
  components: {
    "Meu-Painel": Painel,
    "Imagem-Responsiva": ImagemResponsiva,
    "Meu-Botao": Botao
  },

  data() {
    return {
      titulo: "Alurapic",
      fotos: [],
      filtro: ""
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
  },

  computed: {
    fotosComFiltro() {
      // Se tiver algo preenchido
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  methods: {
    remove(foto) {
      alert("Remover a foto " + foto.titulo);
    }
  }
};
</script>

<style>
.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos-item {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
