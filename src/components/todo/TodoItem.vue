<script setup lang="ts">
interface TodoItem {
  id: string;
  name: string;
  isCompleted: boolean;
}

const props = defineProps({
  todoItem: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});

defineEmits(["delete-task", "mark-completed"]);
</script>

<template>
  <div class="todoItem">
    <input
      type="checkbox"
      :checked="todoItem.isCompleted"
      @click="$emit('mark-completed', index)"
    />
    <span :class="{ completedItem: todoItem.isCompleted }">{{
      todoItem.name
    }}</span>
    <button @click="$emit('delete-task', todoItem.id)">x</button>
  </div>
</template>

<style scoped>
.todoItem {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 10px;
  padding: 3px 0 3px 0;
}
.completedItem {
  text-decoration: line-through;
}
</style>
