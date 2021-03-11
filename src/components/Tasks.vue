<template>
  <div v-for="task in tasks" class="task">
    <span>{{ task.text }} </span>
    <input type="checkbox">
  </div>
</template>


<script>
export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
};
</script>

<style>
.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  line-height: 35px;
  padding: 15px;
}
.task:nth-child(even) {
  background: rgb(249, 247, 247);
}
input[type="checkbox"] {
      width: 30px;
    height: 30px;
    cursor: pointer;
}
</style>
