<template>
    <header>
        <h1>{{title}}</h1>
        <Button
         :text="showAddTask ? 'Close' : 'Add Task'"
          :color="showAddTask ? '#c23616': '#353b48'"
           :toggleShowAdd="toggleShowAdd" />
    </header>
</template>

<script>
import Button from './Button'

export default{
    name: "Header",
    props: {
        title: {
            type: String,
            default: "Task Tracker"
        },
        toggleShowAdd: Function,
        showAddTask: Boolean
    },
    components: {
        Button,
    }
}
</script>

<style scoped>
header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
}
</style>>
