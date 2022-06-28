<template>
    <form @submit="onSubmit">
        <div class="mb-3">
          <label for="task" class="form-label">Task</label>
          <input 
            type="text" 
            class="form-control" 
            id="task"
            placeholder="Add task"
            v-model="task">
        </div>
        <div class="mb-3">
          <label for="date" class="form-label">Date</label>
          <input 
            type="text" 
            class="form-control" 
            id="date"
            placeholder="DD/MM/AAAA HH:MM"
            v-model="date">
        </div>
        <div class="mb-3 form-check">
            <input 
              type="checkbox" 
              class="form-check-input" 
              id="exampleCheck1"
              v-model="reminder">
            <label class="form-check-label" for="exampleCheck1">Set reminder</label>
        </div>
        <button type="submit" class="btn btn-primary">Send Task</button>
    </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
      return {
        task: '',
        date: '',
        reminder: false
      }
    },
    methods: {
      onSubmit(e) {
        e.preventDefault()

        if (this.text !== '') {
          const newTask = {
            id: Math.floor(Math.random() * 100000),
            text: this.task,
            day: this.date,
            reminder: this.reminder          
          }
          this.$emit('add-task', newTask)
        }
      }
    }
}
</script>

<style scoped>
button {
  width: 100%;
}
</style>