<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral />
    </div>
    <div class="column is-three-quarter">
      <FormularioTarefa @ao-salvar-tarefa="salvarTarefa"/>
      <div class="lista">
        <ATarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <MensagemBox v-if="listaEstaVazia">
          Nenhuma tarefa registrada.
        </MensagemBox>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioTarefa from './components/FormularioTarefa.vue';
import ATarefa from './components/ATarefa.vue';
import ITarefa from './interfaces/ITarefa'
import MensagemBox from './components/MensagemBox.vue';

export default defineComponent({
  name: "App",
  data () {
    return {
      tarefas: [] as ITarefa[]
    }
  },
  computed: {
    listaEstaVazia () : boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) : void {
      this.tarefas.push(tarefa)
    }
  },
  components: { BarraLateral, FormularioTarefa, ATarefa, MensagemBox }
});
</script>

<style>
  .lista {
    padding: 1.25rem;
  }
</style>
