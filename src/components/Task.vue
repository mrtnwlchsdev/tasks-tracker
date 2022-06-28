<template>
    <article
        title="Double click to change the reminder" 
        class="main-tasks"
        :class="[task.reminder ? 'reminder' : '', 'main-tasks']"
        @dblclick="onToggle(task.id)" >
        <h3>
            {{task.text}}
            <i 
                class="fas fa-times"
                @click="onDelete(task.id)" >
            </i>
        </h3>
        <span>{{task.day}}</span>   
    </article>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: {}
    },
    methods: {
        onDelete(id) {
            this.$emit('delete-task',id)
        },
        onToggle(id) {
            this.$emit('toggle-reminder', id)
        }
    }
}
</script>

<style scoped>
.main-tasks {
    margin-top: 20px;
    background-color: #efefef;
    padding: 7px 5px;
    cursor: pointer;
    user-select: none;
}

.main-tasks h3 {
    display: flex;
    justify-content: space-between;
}

.main-tasks span {
    display: inline-block;
    margin-top: 5px;
}

.fas {
    color: #E60F0F;
    font-size: 1.4rem;
    cursor: pointer;
}

.reminder {
    border-left: 4px solid #0BBD54;
}
</style>