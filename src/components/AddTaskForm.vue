<template>
  <div class="card mb-4">
    <div class="card-body">
      <form @submit="onSubmit" class="form-inline add-task-form">
        <div class="form-row w-100">
          <div class="form-group col-8">
            <label class="sr-only" for="text">Description</label>
            <input
              type="text"
              v-model="text"
              name="text"
              class="form-control mb-2 mr-sm-2"
              id="text"
              placeholder="Task description"
            />
          </div>

          <div class="form-group col-4 d-flex align-items-center">
            <div class="form-check">
              <input
                name="reminder"
                v-model="reminder"
                class="form-check-input"
                type="checkbox"
                id="reminder"
              />
              <label class="form-check-label" for="reminder"> Reminder </label>
            </div>
          </div>
        </div>

        <button type="submit" class="btn btn-dark w-100">Save Task</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddTaskForm",
  data() {
    return {
      text: "",
      reminder: false
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if(!this.text) {
        alert('please add a task');
        return;
      }
      const newTask = {
        id: Math.floor(Math.random() * 100000),
        text: this.text,
        reminder: this.reminder
      }
      this.$emit('new-task', newTask);
      this.text="";
      this.reminder=false;
    }
  }
};
</script>

<style scoped>
button.w-100 {
  margin: 5px 0;
}
.w-100 {
  width: 100%;
}
.add-task-form {
}
</style>