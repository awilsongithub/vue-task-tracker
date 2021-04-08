


<template>
  <div class="container">
    <Header title="Task Tracker" :showForm='showForm' @toggle-form="toggleAddTaskForm" />
    <AddTaskForm v-show="showForm" @new-task="addNewTask"/>
    <Tasks
      :tasks="tasks"
      @delete-task="this.deleteTask"
      @toggle-reminder="this.toggleReminder"
    />
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css'
import 'jquery/src/jquery.js'
import 'bootstrap/dist/js/bootstrap.min.js'

import Header from "./components/Header";
import Tasks from "./components/Tasks";
import { data } from "./data";
import AddTaskForm from "./components/AddTaskForm";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTaskForm
  },
  data() {
    return {
      tasks: [],
      showForm: false
    };
  },
  methods: {
    deleteTask(id) {
      if (confirm("Delete task?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => 
        task.id === id ? {...task, reminder: !task.reminder } : task
      );
    },
    toggleAddTaskForm() {
      this.showForm = !this.showForm;
    },
    addNewTask(task) {
      this.tasks = [...this.tasks, task];
      this.showForm = false;
    },
    async fetchTasks() {
      const res = await fetch('http://localhost:5000/tasks');
      const data = await res.json();
      return data;
    }
  },
  async created() {
    this.tasks = await this.fetchTasks();
    // [
    //   {
    //     id: 1,
    //     text: "Get Shoulder Fixed",
    //     day: "March 16, 2021",
    //     reminder: true,
    //   },
    //   {
    //     id: 2,
    //     text: "Get Something Done",
    //     day: "March 16, 2021",
    //     reminder: true,
    //   },
    //   {
    //     id: 3,
    //     text: "Get Something Fixed",
    //     day: "March 16, 2021",
    //     reminder: false,
    //   },
    // ];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  padding: 30px;
  border-radius: 5px;
  box-shadow: 0 3px 10px 2px lightgrey;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}

</style>
