<template>
    <MensagemBox>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroTarefa :tempoEmSegundos="tarefa.duracaoEmSegundos" />
            </div>
        </div>
    </MensagemBox>
</template>

<script lang="ts">
import ITarefa from "@/interfaces/ITarefa";
import { defineComponent, PropType } from "vue";
import CronometroTarefa from "./CronometroTarefa.vue";
import MensagemBox from "./MensagemBox.vue";

export default defineComponent({
    name: 'ATarefa',
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    },
    components: { CronometroTarefa, MensagemBox }
})
</script>