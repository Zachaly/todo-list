<template>
    <ul>
        <li :key="task.id" v-for="task in tasks">
            <Task :taskProp="task" @remove-task="this.$emit('remove-task', task.id)"/>
        </li>
    </ul>
</template>

<script>
import Task from './Task.vue'

export default({
    name: "task-list",
    props:{
        tasks: Array
    },
    components:{ Task },
    emits: ['remove-task'],
})
</script>
