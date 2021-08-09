<template>
  <div>
    <label for="todo-input">오늘 할 일 : </label>
    <input type="text" id="todo-input" :value="item" @input="handleInput" />
    <button type="button" @click="addTodo">add</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: ["item"],
  methods: {
    handleInput(e: any) {
      this.$emit("input", e.target.value);
    },
    addTodo() {
      this.$emit("add");
    },
  },
});
</script>

<style scoped></style>
