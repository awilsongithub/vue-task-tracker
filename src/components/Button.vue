<template>
  <button @click="onBtnClick" :style="{ background: color }" class="btn">{{ text }}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: {
      type: String,
      default: "Let's Do This",
    },
    color: {
      type: String,
      default: "black",
    }
  },
  methods: {
    onBtnClick() {
      this.$emit('btn-click');      
    }
  }
};
</script>

<style scoped>

.btn-block {
  display: block;
  width: 100%;
}
</style>