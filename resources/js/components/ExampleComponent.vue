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
    export default {
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
