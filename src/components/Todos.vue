<template>
  <div v-for="todo in todos" :key="todo.id">
    <todo-item :todo="todo" @del-todo="$emit('del-todo', todo.id)"></todo-item>
  </div>
</template>
<script>
import TodoItem from "./TodoItem.vue";
export default {
  props: ["todos"],
  components: { TodoItem },
};
</script>
