<template>
  <div class="container">
    <Header title="Task Tracker" :showAddTask="showAddTask" :toggleShowAdd="toggleShowAdd"  color="#2f3640" />
    <div v-show="showAddTask">
    <AddTask @add-task="addTask" />
    </div>
    <Tasks :toggleReminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"  />
    <Footer />
  </div>
</template>

<script>
import Header from "../components/Header";
import Tasks from "../components/Tasks";
import AddTask from "../components/AddTask";
import Footer from "../components/Footer";
export default {
  name: 'Home',
  components: {
    Header,
    Tasks,
    AddTask,
    Footer,
  },
  data(){
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods:{
    async deleteTask(id) {
      if(confirm('Are you sure to delete this task?')) {
         const res = await fetch(`api/tasks/${id}`, {
           method: 'DELETE'
         })

         res.status === 200
          ? (this.tasks = this.tasks.filter(task => task.id !== id))
           : alert('Error deleting')
      } 
    },

    async toggleReminder(id){
      let taskToToggle = await fetch(`api/tasks/${id}`);
      taskToToggle = await taskToToggle.json();
      const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updTask)
      })

      const data = await res.json()

      this.tasks = this.tasks.map(task => task.id === id ? {...task, reminder: data.reminder} : task);
    },

    async addTask(newTask) {
      const res = await fetch('api/tasks', {
        method: 'post',
        headers: {
          'Content-type': "application/json",
        },
        body: JSON.stringify(newTask)
      })

      const data = await res.json()
    this.tasks = [...this.tasks, data]
    },
    toggleShowAdd() {
    this.showAddTask = !this.showAddTask;
    },

    async fetchTask() {
      const res = await fetch("api/tasks")
      const data = await res.json();
      return data;
    }
  },

  async created() {
    this.tasks = await this.fetchTask()
  }
}
</script>

<style>
.container{
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
}
</style>
