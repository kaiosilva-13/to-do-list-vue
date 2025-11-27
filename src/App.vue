<script setup lang="ts">
import {ref,computed} from 'vue' 
const tarefa = ref <string> ("")
const tarefas = ref <Array<String>> ([])
const valores_logicos = ref <Array <boolean>> ([])
const qtd_tarefas_realizadas = computed (()=>{
  return (valores_logicos.value.filter((elemento) => elemento)).length
})
const qtd_tarefas_totais = computed(() => {
  return valores_logicos.value.length
})
function adicionar_tarefa(){
  if (tarefa.value != ""){
    tarefas.value.push(tarefa.value)
    valores_logicos.value.push(false)
    tarefa.value = ""
  }
}
</script>

<template>
  <form @submit.prevent="adicionar_tarefa">
    <label for="valor">Valor: </label>
    <input type="text" id="valor" v-model="tarefa" placeholder="Digite uma tarefa">
    <input type="submit" value="Adicionar tarefa">
  </form>
  <div>
    <ol>
      <li v-for="(valor, index) in tarefas" :key="index">
        <label :for="'${index}'" :class="{tarefaRealizada: valores_logicos[index]}">{{ valor }}</label>
        <input type="checkbox" :id="'${index}'" v-model="valores_logicos[index]" name="tarefas">
      </li>
    </ol>
  </div>
  <span v-if="qtd_tarefas_totais == 0"> Sem tarefas adicionadas</span>
  <span v-show="qtd_tarefas_totais > 0">
    Tarefas realizadas: {{ qtd_tarefas_realizadas }}/{{ qtd_tarefas_totais }}
  </span>
</template>

<style scoped>
.tarefaRealizada{
  text-decoration: line-through;
  opacity: 0.6;
}
</style>