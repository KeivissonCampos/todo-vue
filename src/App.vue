<script setup>
import { reactive } from 'vue';

const estado = reactive({
    filtro: 'todas',
    tarefas: [
        {
            titulo: 'Estudar ES6',
            finalizada: true,
        },
        {
            titulo: 'Estudar SASS',
            finalizada: false,
        },
        {
            titulo: 'Ir para a academia',
            finalizada: false,
        },
    ],
})

const getTarefasPendentes = () =>{
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () =>{
    const filtro = estado.filtro;
    switch (filtro) {
        case 'pendentes':
            return getTarefasPendentes()
            break;
        case 'finalizadas':
            return getTarefasFinalizadas()
            break;
        default:
            return estado.tarefas
            break;
    }
}

</script>

<template>
    <div class="container">
        <header class="bg-light p-5 mb-4 mt-4 rounded-3">
            <h1>Minhas tarefas</h1>
            <p>
                Você possui {{getTarefasPendentes().length}} tarefas pendentes
            </p>
        </header>
        <form>
            <div class="row">
                <div class="col">
                    <input type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" />
                </div>
                <div class="col-md-2 mb-1 mt-1 mb-md-0 mt-md-0">
                    <select @change="e => estado.filtro = e.target.value" class="form-control">
                        <option value="todas">Todas tarefas</option>
                        <option value="pendentes">Pendentes</option>
                        <option value="finalizadas">Finalizadas</option>
                    </select>
                </div>
                <div class="col-md-2">
                    <button type="submit" class="btn btn-primary">Cadastrar</button>
                </div>
            </div>
        </form>
        <ul class="list-group mt-4 bg-danger">
            <li class="list-group-item" v-for="(tarefa, index) in getTarefasFiltradas()" :key="index">
                <input type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo" />
                <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
                    {{ tarefa.titulo }}
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>

.done{
    text-decoration: line-through;
}

</style>
