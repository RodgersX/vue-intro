<template>
    <div class="todos">
        <div v-for="todo in todos" :key="todo.id">
            <TodoItem :todo="todo" @del-todo="$emit('del-todo', todo.id)"/>
        </div>
    </div>
</template>

<script>
import TodoItem from './todoitem'
export default {
    name: 'todos',
    components: {
        TodoItem
    },
    props: ['todos']
    
}
</script>

<style scoped>

</style>