<template>
    <div class="container">
      <h2>My todolist</h2>
      <table>
        <thead>
            <tr>
                <th>Task</th>
                <th>Due Date</th>
                <th>status</th>
                <th>#</th>
                <th>#</th>
            </tr>    
        </thead>
        <tbody>
            <!-- <tr v-bind:key="todo.id" v-for="todo in todos"> -->
                <Todo v-bind:key="todo.id" v-for="todo in todos" v-bind:todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)" v-on:edit-todo="$emit('edit-todo', todo)"/>
            <!-- </tr> -->
            <!-- <ChildComp @response="(msg) => childMsg = msg" /> -->
                <!-- <Todo @edit-todo="todo"></Todo> -->
        </tbody>
      </table>
      <!-- <ul>
        <li v-bind:key="todo.id" v-for="todo in todos">
          <Todo v-bind:todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)"/>
        </li>
      </ul> -->
    </div>
  </template>

<script>
import Todo from './Todo';

export default {
    name: 'Todos',
    components: {
        Todo
    },
    props: [
        "todos"
    ]
}
</script>

<style>

</style>