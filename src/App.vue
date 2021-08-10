<template>
  <div>
    <header><h1>Vue Todo</h1></header>
    <main>
      <TodoInput :item="todoText" @input="updateTodotext" @add="addTodoItem" />
      <div>
        <ul>
          <TodoListItem
            v-for="(item, idx) in todoItems"
            :key="idx"
            :todoItem="item"
            :index="idx"
            @delete="removeItem"
          />
        </ul>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoListItem from "./components/TodoListItem.vue";

const STORAGE_KEY = "vue-todo-ts-v1";

const storage = {
  save(todoItems: any[]) {
    const parsed = JSON.stringify(todoItems);
    localStorage.setItem(STORAGE_KEY, parsed);
  },
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
    const result = JSON.parse(todoItems);
    return result;
  },
};

export interface Todo {
  title: string;
  done: boolean;
}

export default Vue.extend({
  components: { TodoInput, TodoListItem },
  data() {
    return {
      todoText: "",
      todoItems: [] as Todo[],
    };
  },
  methods: {
    updateTodotext(v: string) {
      this.todoText = v;
    },
    addTodoItem() {
      const value = this.todoText;
      this.todoItems.push({ title: value, done: false });
      storage.save(this.todoItems);
      this.todoText = "";
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch();
    },
    removeItem(index: number) {
      console.log("remove", index);
      this.todoItems.splice(index, 1);
      storage.save(this.todoItems);
    },
  },
  created() {
    this.fetchTodoItems();
  },
});
</script>

<style scoped></style>
