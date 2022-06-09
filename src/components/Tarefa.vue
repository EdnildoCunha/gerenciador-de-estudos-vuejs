<template>
    <Box>
        <div class="columns clicavel" @click="tarefaClicada">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column us-3">
                {{ tarefa.projeto?.nome || 'N/D' }}
            </div>
            <div class="column">
                <Cronometro :tempoSegundos="tarefa.duracaoSegundos" />
            </div>
        </div>
    </Box>
</template>

<script lang="ts">
import ITarefa from '@/interfaces/ITarefa'
import { defineComponent, PropType } from 'vue'
import Box from './Box.vue'
import Cronometro from './Cronometro.vue'

export default defineComponent({
    name: 'Tarefa-Nome',
    emits: ['aoTarefaClicada'],
    components: {
        Cronometro,
        Box
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    },
    methods: {
        tarefaClicada(): void {
            this.$emit('aoTarefaClicada', this.tarefa)
        }
    }
})
</script>

<style scoped>
.clicavel {
    cursor: pointer;
}
</style>
