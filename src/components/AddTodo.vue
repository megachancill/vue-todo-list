<template>
    <div class="container">
        {{ todo }}
        <form @submit="addTodo">
            <input type="text" v-model="todo.name" name="name">
            <input type="date" v-model="duedate">
            <button type="submit">Add</button>
        </form>
        <!-- <input type="text" v-model="todo" placeholder="Enter todo" />
        <input type="date" v-model="duedate" />
        <button @click="addTodo">Add</button> -->
    </div>
  </template>
  <script>
//   import {uuid} from 'uuid';
  import {uuid} from "vue-uuid";

  export default {
    name: 'AddTodo',
    props: ["todo"],
    data() {
        return {
        name: '',
        isEditing: null,
        duedate : null
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodoObj = {
                id: uuid.v4(),
                name: this.name,
                date: this.duedate,
                status: 'true'
            }
            this.$emit('add-todo', newTodoObj);
            this.name = '';
        },
        editTodo(index){
            (this.name = this.todos[index].name), (this.isEditing = index);
        }
    }
    // data() {
    //   return {
    //     name: '',
    //     duedate: null,
    //     statuses: ["to-do", "in-progress", "finished"],
    //   }
    // },
    // methods: {
    // //   addTodo(e) {
    // //     e.preventDefault();
    // //     const newTodoObj = {
    // //       id: uuid.v4(),
    // //       name: this.name,
    // //       status: "to-do"
    // //     }
    // //     this.$emit('add-todo', newTodoObj);
    // //     this.name = '';
    // //   }
    //     addTodo() {
    //         if (this.todo.length === 0) return;
    //         if (this.isEditing != null) {
    //             this.todos[this.isEditing].name = this.todo;
    //             this.isEditing = null;
    //         } else {
    //             this.todos.push({
    //             name: this.todo,
    //             date: this.duedate,
    //             status: "to-do",
    //             });
    //         }
    //         this.$emit('add-todo', newTodoObj);
    //         this.todo = "";
    //     }
    // }
  }
  </script>
  <style scoped>
  </style>