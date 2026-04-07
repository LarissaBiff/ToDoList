<script setup>
import { ref } from 'vue';
const tarefas = ref([
    { id: 1, desc: 'Prova Geografia', status: 'pendente' },
    { id: 2, desc: 'Prova História', status: 'concluida' },
    { id: 3, desc: 'Trabalho DevWeb', status: 'pendente' },
]);

let novaTarefa = ref('');

let posicao_alterar = ref(-1);

function addTarefa() {
    if (posicao_alterar.value == -1) {
        let maiorID = Math.max(...tarefas.value.map(item => item.id));
        tarefas.value.push({
            id: maiorID + 1,
            desc: novaTarefa.value,
            status: 'pendente'
        });
    } else {
        tarefas.value[posicao_alterar.value].desc =  novaTarefa.value
        posicao_alterar.value = -1
    }
    
    novaTarefa.value = '';
}

function deleteTarefa(item) {
    const posicao = tarefas.value.findIndex(t => t.id === item.id);
    tarefas.value.splice(posicao, 1);
}

function editTarefa(item) {
    posicao_alterar.value = tarefas.value.findIndex(t => t.id === item.id);
    novaTarefa.value = tarefas.value[posicao_alterar.value].desc;

}

function marcarConcluida(id) {
    const posicao = tarefas.value.findIndex(t => t.id == id);
    if (tarefas.value[posicao].status=='pendente'){
        tarefas.value[posicao].status = 'concluida';
    } else {
        tarefas.value[posicao].status = 'pendente';
    }
}

function pesquisarTarefa() {
    const termo = novaTarefa.value.toLowerCase();
    return tarefas.value.filter(t => t.desc.toLowerCase().includes(termo));
}
</script>

<template>
<div class="container">
    <h1>Lista de Tarefas</h1>
    <div class="addd">
        <input type="text" v-model="novaTarefa" placeholder="tarefa">
        <button @click="addTarefa">Add</button>
    </div>
    <ul>
        <li v-for="item in tarefas" 
        :key="item.id" >

            <span
            @click="marcarConcluida(item.id)"
            :class="{concluida: item.status=='concluida'}">
                {{ item.desc }}
            </span>

            <span>
                <a href="#" @click.prevent="deleteTarefa(item)">Delete</a>
                <a href="#" @click.prevent="editTarefa(item)">Edit</a>
            </span>
            
        </li>
    </ul>

</div>
</template>

<style scoped>
template {
    align-items: center;
    display: flex;
    justify-content: center;
    
}
div.container {
    background-color: rgb(179, 46, 68);
    padding: 1rem 4rem 2rem 4rem;
    border-radius: 15px;
}
div.container h1 {
    color: rgb(133, 206, 133);
    text-align: center;
    padding: 0 0 1rem 0;
    font-weight: bolder;
}
div.container ul {
    padding: 0.8vw 0 0 0;
}
/* Estilo */

div.container ul li {
    cursor: pointer;
}
.concluida {
    text-decoration: line-through;
}

/* Estilo */

div.container div.addd{
    display: flex;
    gap: 0.5vw;
}
div.container div.addd input {
    border: none;
    border-radius: 5px;
    padding: 5px 10px;
    color: rgba(218, 0, 54, 0.932);
}
input::placeholder {
  color: rgb(218, 0, 55);
  opacity: 0.7;
  font-weight: bold;
}
div.container div.addd button{
    border: none;
    border-radius: 5px;
    padding: 5px 10px;
    color: rgba(218, 0, 54, 0.932);
    font-weight: bolder;
    background-color: rgb(255, 255, 255);
}

div.container ul span a {
    margin-left: 1vw;
    color: rgb(133, 206, 133);
}
</style>
