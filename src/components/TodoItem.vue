<template>
    <div v-bind:class="{'is-completed': todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)">x</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: [
      "todo"
    ],
    methods: {
        markComplete() {
            //console.log('test Alex');
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style scoped>
    .is-completed {
        text-decoration: line-through;
    }
</style>