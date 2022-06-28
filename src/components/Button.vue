<template>
    <button
        class="btn"
        @click="onClick"
        :style="{background: color}">
        {{text}}
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        color: String,
        text: String,
        showAddTask: Boolean
    },
    methods: {
        onClick() {
            this.$emit('btn-click')
        }
    }
}
</script>

<style scoped>
.btn {
    padding: 9px 7px;
    color: #fff;
    background-color: #000;
    border-radius: 10px;
    font-size: 1.02rem;
    font-weight: 900;
    cursor: pointer;
}
</style>