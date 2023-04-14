<template>
    <div>
        <h1>{{ title }}</h1>
        <div class="todo-list">
            <div v-for="(todo, key) in todos" class="todo" :key="key">
                <input v-model="todo.label" readonly class="input-label" placeholder="label" type="text"/>
                <input v-model="todo.manager" readonly class="input-manager" placeholder="manager" type="text"/>
                <input v-model="todo.hours" readonly class="input-hours" placeholder="hours" type="number"/>
                <button>Editer</button>
            </div>
        </div>
        <div class="todo-form">
            <input v-model="label" class="input-label" placeholder="label" type="text"/>
            <input v-model="manager" class="input-manager" placeholder="manager" type="text"/>
            <input v-model="hours" class="input-hours" placeholder="hours" type="number"/>
            <button @click="addTodo" class="submit-btn">Ajouter</button>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue';

const title = ref('TODO LIST');
const label = ref('');
const manager = ref('');
const hours = ref(0);

const todos = ref([]);

function addTodo() {
    todos.value.push({label, manager, hours});
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
</style>