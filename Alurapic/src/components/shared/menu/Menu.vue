<template>
    <nav>
      <ul>
        <li v-for="rota in rotas" :key="rota">
          <router-link :to="rota.path ? rota.path : '/'">{{
            rota.titulo
          }}</router-link>
        </li>
        <!-- <p>{{ route.path }}</p> -->
        <!-- <li><router-link to="/cadastro">Cadastro</router-link></li> -->
      </ul>
    </nav>
</template>

<script>
export default {
    props: {
        rotas: {
            required: true,
            type: Array,
        }
    }
}
</script>

<style>

</style>