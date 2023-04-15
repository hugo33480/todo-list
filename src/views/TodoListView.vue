<template>
    <div>
        <h1>{{ title }}</h1>
        <span>Total: {{ count }}</span>
        <div class="todo-list">
            <div v-for="(todo, key) in todos" class="todo" :key="key">
                <input v-model="todo.label" class="input-label" placeholder="label" type="text"/>
                <input v-model="todo.manager" class="input-manager" placeholder="manager" type="text"/>
                <input v-model="todo.hours" class="input-hours" placeholder="hours" type="number"/>
                <button @click="deleteTodo(key)" class="btn-delete">&times;</button>
            </div>
        </div>
        <div class="todo-form">
            <form @submit.prevent="addTodo">
                <input v-model="label" class="input-label" placeholder="label" type="text"/>
                <input v-model="manager" class="input-manager" placeholder="manager" type="text"/>
                <input v-model="hours" class="input-hours" placeholder="hours" type="number"/>
                <button type="submit" class="submit-btn">Ajouter</button>
            </form>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue';

const title = ref('TODO LIST');
const label = ref('');
const manager = ref('');
const hours = ref(null);

const todos = ref([]);

const count = ref(0);

function addTodo() {
    todos.value.push({label: label.value, manager: manager.value, hours: hours.value});
    count.value++;
}

function deleteTodo(key) {
    todos.value.splice(key, 1);
    count.value--;
}

</script>

<style scoped>
.todo-list {
    margin-bottom: 10px;
}

.todo {
    margin-bottom: 10px;
}

.input-label {
    margin-right: 5px
}

.input-manager {
    margin-right: 5px;
    margin-left: 5px;
}

.input-hours {
    margin-left: 5px;
}

.submit-btn {
    margin-left: 10px;
}

.btn-delete {
    width: 58px;
    margin-left: 10px;
}
</style>