<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @ao-tema-alterado="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
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
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
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
    },
    trocarTema (modoEscuroAtivo: boolean) : void {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  },
  components: { BarraLateral, FormularioTarefa, ATarefa, MensagemBox }
});
</script>

<style>
  .lista {
    padding: 1.25rem;
  }
  main {
    --bg-primario: #fff;
    --texto-primario: #000;
  }
  main.modo-escuro {
    --bg-primario: #2B2D42;
    --texto-primario: #DDD;  
  }
  .conteudo {
    background-color: var(--bg-primario);
  }
</style>