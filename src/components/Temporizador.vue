<template>
    <section class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoSegundos="tempoSegundos" />
        <Botao @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />
        <Botao @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
    </section>
</template>


<script lang="ts">
import { defineComponent } from 'vue';
import Botao from './Botao.vue';
import Cronometro from './Cronometro.vue';

export default defineComponent({
    name: "Temporizador-Nome",
    emits: ['aoTemporizadorFinalizado'],
    Components: {
        Cronometro
    },
    data() {
        return {
            tempoSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        };
    },
    methods: {
        iniciar() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoSegundos += 1;
            }, 1000);
        },
        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro);
            this.$emit('aoTemporizadorFinalizado', this.tempoSegundos)
            this.tempoSegundos = 0
        }
    },
    components: { Cronometro, Botao }
})
</script>