<template>
    <button :class="estiloDoBotao" :type="tipo" @click="disparaAcao()"> {{ rotulo }} </button>
</template>

<script>
export default {
    props: ['tipo', 'rotulo', 'confirmacao', 'estilo'],

    methods: {
        disparaAcao() {
            if(this.confirmacao) {
                if(confirm('Deseja mesmo remover essa foto?')) {
                    this.$emit('botaoAtivado');
                }
                return;
            }
            this.$emit('botaoAtivado')
        }
    },

    computed: {
        estiloDoBotao() {
            if(this.estilo == 'padrao' || !this.estilo) return 'botao botao-padrao';
            if (this.estilo == 'perigo') return 'botao botao-perigo';
        }
    }
}
</script>

<style>
    .botao {
        display: inline-block;
        padding: 10px;
        border-radius: 3px;
        margin: 10px;
        font-size: 1.2em;
    }

    .botao-perigo {
        background-color: firebrick;
        color: white;
    }

    .botao-padrao {
        background-color: darkcyan;
        color: white;
    }
</style>