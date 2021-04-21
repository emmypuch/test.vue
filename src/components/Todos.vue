<template>
    <div>
        <div v-for="(todo, index) in todos" v-bind:key="index">
            <!-- <h3>{{ todo.title }}</h3> -->
            <TodoItem v-bind:todo="todo" v-bind:index="index" v-on:del-todo="$emit('del-todo', $event)"/>
        </div>
    </div>
</template>

<script>
import TodoItem from "./Todoitem.vue"
export default {
    name: "Todos",
    props: ["todos"],
    components: {
        TodoItem
    }
}
</script>

<style scoped>

</style>
