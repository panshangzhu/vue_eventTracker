<template>
<div>
    <div :key="task.id" v-for="task in tasks">
        <Task @toggle-reminder="toggleReminder" @delete-task="$emit('delete-task', task.id)" :task="task" />
    </div>
</div>
</template>

<script>
import Task from "./Task"
export default{
    name: 'Tasks',
    props: {
        tasks: Array,
        toggleReminder: Function,
    },
    components: {
        Task
    },
    emits:['delete-task'],
}
</script>