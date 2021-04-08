<template>
  <div :key="task.id" v-for="task in tasks">
    <Task :task="task" @delete-task="deleteTask" @toggle-reminder="toggleReminder" />
  </div>
</template>

<script>
import Task from "./Task";

export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  methods: {
    deleteTask(id) {
      this.$emit('delete-task', id);
    },
    toggleReminder(id) {
      this.$emit('toggle-reminder', id);
    }
  },
  created() {
    console.log(this.props);
  },
  emits: ["delete-task", 'toggle-reminder'],
};
</script>



