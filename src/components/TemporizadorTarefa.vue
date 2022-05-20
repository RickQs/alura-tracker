<template>
    <CronometroTarefa :tempo-em-segundos="tempoEmSegundos" />
    <button class="button" @click="iniciar" :disabled="cronometroRodando">
        <span class="icon">
            <i class="fas fa-play"></i>
        </span>
        <span>play</span>
    </button>
    <button class="button" @click="finalizar" :disabled="!cronometroRodando">
        <span class="icon">
            <i class="fas fa-stop"></i>
        </span>
        <span>stop</span>
    </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CronometroTarefa from "./CronometroTarefa.vue";

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
    components: { CronometroTarefa }
})
</script>