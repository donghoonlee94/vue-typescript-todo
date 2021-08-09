<template>
  <div>
    <h1>Vue Todo</h1>
    <TodoInput :item="todoText" @input="updateTodotext" @add="addTodoItem" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";

export default Vue.extend({
  components: { TodoInput },
  data() {
    return {
      todoText: "",
    };
  },
  methods: {
    updateTodotext(v: any) {
      this.todoText = v;
    },
    addTodoItem() {
      const value = this.todoText;
      localStorage.setItem(value, value);
      this.todoText = "";
    },
  },
});
</script>

<style scoped></style>
