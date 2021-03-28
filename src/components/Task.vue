<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
        <div class="firstLayer">
        <h3>
            {{ task.text }}
        </h3>
        <i @click="$emit('delete-task')" class="fas fa-times"></i>
        </div>
        <p>{{ task.day }}</p>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object
    },
}
</script>

<style scoped>
.task {
    background: #7f8fa6;
    padding: 16px;
    margin-bottom: 8px;
    display: flex;
    flex-direction: column;
}
i{
    cursor: pointer;
    font-size: 20px;
}
.firstLayer{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.firstLayer i {
    color: #c23616
}
.task.reminder {
    border-left: 5px solid #e84118;
}
</style>