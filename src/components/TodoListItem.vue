<template>
  <li>
    <span>{{ todoItem }}</span>
    <button @click="removeItem">삭제</button>
  </li>
</template>

<script lang="ts">
import Vue, { PropType } from "vue";
import { Todo } from "../App.vue";

export default Vue.extend({
  props: {
    todoItem: Object as PropType<Todo>,
    index: Number,
  },
  methods: {
    removeItem() {
      this.$emit("delete", this.index);
    },
  },
});
</script>

<style scoped></style>
