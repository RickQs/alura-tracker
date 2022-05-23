<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral />
    </div>
    <div class="column is-three-quarter">
      <FormularioTarefa @ao-salvar-tarefa="salvarTarefa"/>
      <div class="lista">
        <ATarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
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

export default defineComponent({
  name: "App",
  data () {
    return {
      tarefas: [] as ITarefa[]
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) : void {
      this.tarefas.push(tarefa)
    }
  },
  components: { BarraLateral, FormularioTarefa, ATarefa }
});
</script>

<style>
  .lista {
    padding: 1.25rem;
  }
</style>
