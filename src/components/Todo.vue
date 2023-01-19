<template>
    <tr>
        <td v-bind:class="{ 'status': todo.status }">
            {{ todo.id }}
            <span v-on:click="markStatus">{{ todo.name }}</span>
        </td>
        <td>
            {{ todo.duedate }}
        </td>
        <td>
            <span>{{ todo.status }}</span>
        </td>
        <td>
            <button @click="$emit('delete-todo', todo.id)">Delete</button>
            <!-- <button>Delete</button> -->
        </td>
        <td>
            <button @click="editTodo()">Edit</button>
        </td>
        <!-- {{todo}} -->
    </tr>
    <!-- <div v-bind:class="{ 'completed': todo.completed }">
      <p v-on:click="markComplete">{{ todo.title }}</p>
      <button @click="$emit('delete-todo', todo.id)">Delete</button>
    </div> -->
</template>
<script>
    export default {
        emits: ['edit-todo'],
        name: "Todo",
        props: ["todo"],
        isEditing: null,
        methods: {
            markStatus() {
                this.todo.status = !this.todo.status;
            },
            editTodo() {
                this.$emit('edit-todo', this.todo);
            },
        },
    };
</script>
<style scoped>
    .status {
        text-decoration: line-through;
    }
</style>
