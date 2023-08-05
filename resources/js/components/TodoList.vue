<template>
    <div>
        <h1>Lista de Tareas</h1>
        <input type="text" v-model="newTaskTitle" @keyup.enter="addTask">
        <button @click="addTask">Añadir tarea</button>

        <ul>
            <li v-for="task in tasks" :key="task.id">
                <input type="checkbox" v-model="task.completed" @change="updateTask(task)">
                {{ task.title }}
                <button @click="deleteTask(task)">Eliminar</button>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            tasks: [],
            newTaskTitle: '',
        };
    },
    async created() {
        const response = await axios.get('/api/tasks');
        this.tasks = response.data;
    },
    methods: {
        async addTask() {
            const response = await axios.post('/api/tasks', {
                title: this.newTaskTitle,
            });

            this.tasks.push(response.data);
            this.newTaskTitle = '';
        },
        async updateTask(task) {
            await axios.put('api/tasks/${task.id}', task);
        },
        async deleteTask(task) {
            await axios.delete('api/tasks/${task.id}');
            this.tasks = this.tasks.filter(t => t.id !== task.id);
        },
    },
};
</script>
