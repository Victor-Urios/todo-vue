<script setup>
import { reactive } from 'vue';
import Cabeçalho from './components/Cabeçalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive( { 
  filtro: 'todas',
  tarefaTemp: '',
    tarefas: [ 
      {
        titulo: 'Estudar EcmaScript6',
        finalizada: false, 
      },
      { 
        titulo: 'Estudas SASS',
        finalizada: false,
      },
      { 
        titulo: 'Ir para a academia',
        finalizada: true,
      }
    ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}
const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = { 
    titulo: estado.tarefaTemp,
    finalizada: false, 
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}

</script>

<template>
<div class="container">
  <Cabeçalho :tarefas-pendentes="getTarefasPendentes().length" />
  <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
  <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
</div>
</template>


