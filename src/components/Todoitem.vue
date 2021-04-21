<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">
            {{ todo.title }}
            <button @click="$emit('del-todo', index)" class="del">x</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo", "index"],
    methods: {
        markComplete () {
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style scoped>
    .todo-item {
        padding: 10px;
        background: #f4f4f4;
        border-bottom: 1px solid #ccc;
    }

    .is-complete {
        text-decoration: line-through;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        float: right;
        cursor: pointer;
    }
</style>