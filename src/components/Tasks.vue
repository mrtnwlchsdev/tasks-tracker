<template>
    <section 
        v-for="task in tasks"
        :key="task.id">
        <Task 
            :task="task"
            @delete-task="$emit('delete-task', task.id)"
            @toggle-reminder="$emit('toggle-reminder', task.id)" />
    </section>
</template>

<script>
import Task from '@/components/Task.vue'

export default {
    name: 'Tasks',
    components: {
        Task
    },
    props: {
        tasks: Array
    },
    emits: ['delete-task','toggle-reminder']
}
</script>

<style scoped>
</style>