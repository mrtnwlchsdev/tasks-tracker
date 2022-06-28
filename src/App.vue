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
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
      })
    },
    toggleReminder(id) {
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
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 3rd at 1:30pm',
        reminder: true
      },
      {
        id: 3,
        text: 'Visit Grandparents',
        day: 'March 5th at 12:00pm',
        reminder: false
      }
    ]
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