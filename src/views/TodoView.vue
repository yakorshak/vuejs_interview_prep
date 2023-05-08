<script setup lang="ts">
import { reactive, ref } from "vue";
import TodoInput from "../components/todo/TodoInput.vue";
import TodoItem from "../components/todo/TodoItem.vue";
import { uid } from "uid";
interface TodoItem {
  id: string;
  name: string;
  isCompleted: boolean;
}

let todoItems = ref<TodoItem[]>([]);

const addTask = (text: string) => {
  todoItems.value.push({
    id: uid(),
    name: text,
    isCompleted: false,
  });
};

const markCompleted = (index: number) => {
  todoItems.value[index].isCompleted = !todoItems.value[index].isCompleted;
};

const deleteTask = (id: string) => {
  todoItems.value = todoItems.value.filter((todo) => todo.id != id);
};
</script>

<template>
  <div class="container">
    <TodoInput @create-todo="(text) => addTask(text)" />
    <TodoItem
      v-for="(item, index) in todoItems"
      :todo-item="item"
      :index="index"
      @delete-task="(id: string) => deleteTask(id)"
      @mark-completed="(index: number) => markCompleted(index)"
    ></TodoItem>
  </div>
</template>

<style scoped></style>
