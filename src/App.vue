<script setup>
import { ref } from 'vue';
const tarefa = ref([
    { id: 1, desc: 'Prova Geografia', status: 'pendente' },
    { id: 2, desc: 'Prova História', status: 'concluida' },
    { id: 3, desc: 'Trabalho DevWeb', status: 'pendente' },
]);
</script>

<template>
<div class="container">
    <ul>
        <li v-for="item in tarefas" :key="item.id">
            {{ item.desc }}
        </li>
    </ul>
</div>
</template>

<style scoped>
</style>
