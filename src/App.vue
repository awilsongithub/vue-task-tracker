


<template>
  <div class="container">
    <Header
      title="Task Tracker"
      :showForm="showForm"
      @toggle-form="toggleAddTaskForm"
    />
    <AddTaskForm v-show="showForm" @new-task="addNewTask" />
    <Tasks
      :tasks="tasks"
      @delete-task="this.deleteTask"
      @toggle-reminder="this.toggleReminder"
    />
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.min.css";
import "jquery/src/jquery.js";
import "bootstrap/dist/js/bootstrap.min.js";

import Header from "./components/Header";
import Tasks from "./components/Tasks";
import { data } from "./data";
import AddTaskForm from "./components/AddTaskForm";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTaskForm,
  },
  data() {
    return {
      tasks: [],
      showForm: false,
    };
  },
  methods: {
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
    toggleAddTaskForm() {
      this.showForm = !this.showForm;
    },
    async fetchTasks() {
      const sortQueryString = "?_sort=text";
      const res = await fetch(`api/tasks${sortQueryString}`);
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
    async addNewTask(task) {
      const options = {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      };
      const res = await fetch("api/tasks", options);
      const data = await res.json();
      this.tasks = [...this.tasks, await data];
      this.showForm = false;
    },
    async deleteTask(id) {
      if (confirm("Delete task?")) {
        const res = await fetch(`api/tasks/${id}`, { method: "DELETE" });
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task");
      }
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
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
