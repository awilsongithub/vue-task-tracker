<template>
  <header>
    <h1>{{ title }}</h1>
    <Button :text="showForm ? 'Close' : 'Add Task'" @btn-click="$emit('toggle-form')" />
  </header>
</template>

<script>
import Button from "./Button";
import $ from "jquery";

export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "John Doe",
    },
    showForm: false,
  },
  components: {
    Button,
  },
  methods: {
    getButtonText() {
      return this.showForm ? "Close Form" : "Add Task";
    },
  },
  mounted() {
    $("button").addClass("btn-dark w-125px");
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.w-125px {
  width: 125px;
}
</style>