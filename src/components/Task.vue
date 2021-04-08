<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3 class="title-and-icon">
      {{ task.text }}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times" />
    </h3>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  }
};
</script>

<style scoped>
.task {
  line-height: 35px;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 5px;
  background: #f1f1f1;
}
.title-and-icon {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
.task:nth-child(even) {
  background: rgb(249, 247, 247);
}
.fas.fa-times {
  cursor: pointer;
}
.task.reminder {
  border-left: 8px solid green;
}
.fas {
  color: red;
}
</style>