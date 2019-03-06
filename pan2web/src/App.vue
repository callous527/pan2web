<template>
  <div>
    <TodoInput/>
    <ul>
      <TodoItem/>
    </ul>
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";
import TodoItem from "./components/TodoItem.vue";
export default {
  components: {
    TodoInput,
    TodoItem,
  }
};
</script>