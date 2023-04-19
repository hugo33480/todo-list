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
                <select v-model="manager" class="input-manager">
                    <option v-for="(manager, key) in managers" :key="key">{{ manager }}</option>
                </select>
                <input v-model="hours" class="input-hours" placeholder="hours" type="number"/>
                <button type="submit" class="submit-btn">Ajouter</button>
            </form>
        </div>
        <span v-for="(error, key) in errors" :key="key" class="errors">{{ error }}</span>
    </div>
</template>

<script setup>
import {ref, toRaw} from 'vue';

const managers = [
    "Hugo",
    "Sophie",
    "Daniel",
    "Didier",
    "Pascal"
];

const title = ref('TODO LIST');
const label = ref('');
const manager = ref('');
const hours = ref(null);
const todos = ref([]);
const count = ref(0);
const errors = ref([]);

function addTodo() {
    errors.value = [];

    const managerTaskCount = todos.value.reduce((count, it) => {
        if(toRaw(it).manager === manager.value)
            return count + 1;
    }, 0);

    const managerHoursCount = todos.value.reduce((count, it) => {
        if(toRaw(it).manager === manager.value)
            return count + it.hours;
    }, hours.value || 0);

    if(!label.value.length || !manager.value.length || !hours.value) {
        errors.value.push("Veuillez saisir tout les champs \n");
    } else if(managerTaskCount >= 3) {
        errors.value.push("Ce manager a dejà 3 tâches \n");
    } else if(managerHoursCount > 10) {
        errors.value.push("Le nombre d'heures dépasse 10h pour ce manager \n");
    } else {
        todos.value.push({label: label.value, manager: manager.value, hours: hours.value});
        count.value++;
        errors.value = [];
    }
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
    width: 177px;
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

.errors {
    color: red;
}

.todo-form {
    margin-bottom: 10px;
}
</style>