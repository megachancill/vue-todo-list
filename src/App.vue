<template>
  <div id="app">
    <AddTodo :todo="todo" v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" v-on:edit-todo="editTodo"/>
  </div>
</template>

<script>
  import {uuid} from "vue-uuid";
  import Todos from './components/Todos';
  import AddTodo from './components/AddTodo';
  export default {
    name: 'app',
    components: {
      Todos,
      AddTodo
    },
    data() {
      return {
        todo: {},
        todos: [
          {
            id: 1,
            name: 'Go workout',
            duedate: '01-21-2023',
            status: "to-do",
            completed: false
          },
          {
            id: 2,
            name: 'Do laundry',
            duedate: '01-21-2023',
            status: "to-do",
          },
          {
            id: 3,
            name: 'Cook food',
            duedate: '01-21-2023',
            status: "to-do",
          },
          {
            id: 4,
            name: 'Clean up room',
            duedate: '01-21-2023',
            status: "in-progres",
          },
          {
            id: 5,
            name: 'Finish work',
            duedate: '01-21-2023',
            status: "finished",
          }
        ],
      }
    },
    methods: {
      addTodo(newTodoObj) {
        this.todos = [...this.todos, newTodoObj];
      },
      deleteTodo(todoId) {
        this.todos = this.todos.filter(todo => todo.id !== todoId);
      },
      editTodo(index){
        (this.todo = index)
      }
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center; 
  color: #2c3e50;
  margin-top: 60px;
}
</style>
