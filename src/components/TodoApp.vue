<template>
  <div class="container">
    <h1>Todo List</h1>
    <input type="text" v-model="todo" placeholder="Enter todo" />
    <input type="date" v-model="duedate" />
    {{ currentDate() }}
    <!-- rubah background list sesuai tanggal jika belum deadline warna hijau, hari h default, sudah telat warna merah -->
    <button @click="storeTodo">Add</button>
    <!-- list data -->
    <table class="table">
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
        <tr v-for="(todo, index) in todos" :key="index">
          <td>
            <span :class="{ 'line-through': todo.status === 'finished' }">
              {{ todo.name }}
            </span>
          </td>
          <td>
            <!-- due date rubah warna background hijau untuk belum merah untuk lewat deadline-->
            <!-- {{todo.date}} -->
            <span
              :class="{
                'text-danger': compareDate(todo.date) == 'past',
                'text-success': compareDate(todo.date) == 'future',
                'text-default': compareDate(todo.date) == 'present',
              }"
            >
              {{ compareDate(todo.date) }}
              {{ todo }}
            </span>
            <!-- <span :style="colorDate">{{todo.date}}</span> -->
            <!-- {{todo.date}} -->
          </td>
          <td>
            <span
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': todo.status === 'to-do',
                'text-success': todo.status === 'finished',
                'text-warning': todo.status === 'in-progress',
              }"
            >
              {{ capitalizeFirstChar(todo.status) }}
            </span>
          </td>
          <td>
            <button @click="editTodo(index)">Edit</button>
          </td>
          <td>
            <button @click="removeTodo(index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- <ol>
            <li v-for="(todo, index) in todos">
                <span :class="{'line-through': todo.status === 'finished'}">
                    {{ todo.name }}
                </span>
                |<span class="pointer noselect" @click="changeStatus(index)" :class="{ 'text-danger': todo.status === 'to-do', 'text-success': todo.status === 'finished', 'text-warning': todo.status === 'inprogress',}">
                    {{capitalizeFirstChar(todo.status)}}
                </span>
                |<button @click="editTodo(index, todo)">Edit</button>
                |<button @click="removeTodo(index)">Delete</button>
            </li>
        </ol> -->
  </div>
</template>

<script>
export default {

    data(){
        return{
            isEditing: null,
            todo: "",
            duedate: null,
            selectedTodo: null,
            statuses: ["to-do", "in-progress", "finished"],
            /* Status could be: 'to-do' / 'in-progress' / 'finished' */
            todos: [
            {
                name: "Steal bananas from the supermarket.",
                status: "to-do",
            },
            {
                name: "Eat 1 kg chocolate in 1 hour.",
                status: "in-progress",
            },
            {
                name: "Create YouTube video.",
                status: "finished",
            },
            ],
        };
    },

  methods: {
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.todos[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.todos[index].status = this.statuses[newIndex];
    },

    removeTodo(index) {
      this.todos.splice(index, 1);
    },

    editTodo(todo) {
      console.log(todo, 'todo')
      (this.todo = todo)  
    },

    storeTodo() {
      if (this.todo.length === 0) return;
      if (this.isEditing != null) {
        this.todos[this.isEditing].name = this.todo;
        this.isEditing = null;
      } else {
        this.todos.push({
          name: this.todo,
          date: this.duedate,
          status: "to-do",
        });
      }
      this.todo = "";
    },
    compareDate(val) {
      var today = new Date();
      today.setHours(0, 0, 0, 0);
      var target = new Date(val);
      target.setHours(0, 0, 0, 0);

      console.log(today, "today");
      console.log(target, "target");
      if (today > target) {
        return "past";
      } else if (today < target) {
        return "future";
      } else {
        return "present";
      }
    },
    currentDate() {
      const current = new Date();
      // const currentdate = `${current.getFullYear()}-${current.getMonth()+1}-${current.getDate()}`;
      const currentDate = new Date(current);
      return currentDate;
    },
  },
};
</script>

<style></style>
