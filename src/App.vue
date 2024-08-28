<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formu from './components/Formu.vue';
import Lista from './components/Lista.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar EcmaScript6',
      finalizada: false
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false
    },
    {
      titulo: 'Jogar CS',
      finalizada:true
    }
  ]
})

const getPend = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getFinalidas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getFiltradas = () => {
  const { filtro } = estado;
  //const filtro = estado.filtro;

  switch (filtro) {
    case 'pendentes':
      return getPend();
    case 'finalizadas':
      return getFinalidas();
    default:
      return estado.tarefas
  }
}

const cadastrarTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pend="getPend().length"/>
    <Formu :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastrarTarefa" />
    <Lista :tarefas="getFiltradas()"/>

  </div>
</template>
