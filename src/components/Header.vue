<template>
    <div>
        <header>
            <h1>{{title}}</h1>
            <Button
                :showAddTask="showAddTask"
                :text="showAddTask ? 'Close' : 'Add Task'"
                :color="showAddTask ? '#E60F0F' : '#0BBD54'"
                @btn-click="$emit('show-form')" />
        </header>
    </div>
</template>

<script>
import Button from '@/components/Button.vue'

export default {
    name: 'Header',
    props: {
        title: String,
        showAddTask: Boolean
    },
    components: {
        Button
    },
    emits: ['show-form']
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>