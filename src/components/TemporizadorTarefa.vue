<template>
    <CronometroTarefa :tempo-em-segundos="tempoEmSegundos" />
    <BotaoExecucao @clicado="iniciar" :desabilitado="cronometroRodando" texto="play" icone="fas fa-play" />
    <BotaoExecucao @clicado="finalizar" :desabilitado="!cronometroRodando" texto="stop" icone="fas fa-stop" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CronometroTarefa from "./CronometroTarefa.vue";
import BotaoExecucao from "./BotaoExecucao.vue";

export default defineComponent({
    name: "TemporizadorTarefa",
    emits: ['aoTemporizadorFinalizado'],
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        };
    },
    methods: {
        iniciar(): void {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos++;
            }, 1000);
        },
        finalizar(): void {
            this.cronometroRodando = false
            clearInterval(this.cronometro);
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    },
    components: { CronometroTarefa, BotaoExecucao }
})
</script>