<script setup lang="ts">
import { reactive } from "vue";
const currentItemState = reactive({
  text: "",
});

const emitCreateTodo = defineEmits(["create-todo"]);
const createTodo = () => {
  emitCreateTodo("create-todo", currentItemState.text);
  currentItemState.text = "";
};
</script>

<template>
  <div class="todoInput">
    <input
      v-model="currentItemState.text"
      type="text"
      placeholder="type a task here"
    />
    <button @click="createTodo()">Add Todo</button>
  </div>
</template>

<style scoped>
.todoInput {
  display: block;
}
input {
  margin: 10px 10px 10px 0;
}
</style>
