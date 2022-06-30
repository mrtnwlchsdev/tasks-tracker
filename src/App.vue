<template>
  <main class="main">
    <Header 
      title="TASKS"
      :showAddTask="showAddTask"
      @show-form="showForm" />
    <div v-if="showAddTask">
      <AddTask 
        @add-task="addTask"/>
    </div>
    <Tasks 
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder" />
  </main>
</template>

<script>
import Header from '@/components/Header'
import Tasks from '@/components/Tasks.vue'
import AddTask from '@/components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    async addTask(task) {
      const response = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(task)
      })
      const data = await response.json()

      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id) {
      const response = await fetch(`api/tasks/${id}`, {
        method: 'DELETE'
      })
      if (response.status === 200) {
        this.tasks = this.tasks.filter((task) => {
          return task.id !== id
        })
      }
    },    
    async fetchTasks() {
      const response = await fetch('api/tasks')
      const data = await response.json()
      return data
    },
    async toggleReminder(id) {
      const fetchTasks = await this.fetchTasks()
      let updateData
      fetchTasks.forEach(task => {
        if (task.id === id) {
          updateData = {...task, reminder: !task.reminder}
        }
      })

      fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(updateData)
      })  

      this.tasks = this.tasks.map((task) => {
        if (task.id === id) {
          return {...task, reminder: !task.reminder}
        } else {
          return task
        }
      })
    },
    showForm() {
      this.showAddTask = !this.showAddTask
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Anek+Latin:wght@500&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Anek Latin', monospace;
  transition: all .2s linear;
}

html {
  font-size: 1em;
}

.main {
  margin: 20px;
  padding: 10px;
  border: 1px solid #c2c2c2;
}
</style>