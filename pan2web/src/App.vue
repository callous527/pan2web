<template>
  <div>
    <TodoInput/>
    <ul>
      <TodoItem v-for="todo in todos" :data="todo"/>
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
  },
  data(){
    return {
      todos: ['123','456'],
    };
  }
};
</script>