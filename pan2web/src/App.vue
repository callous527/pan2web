<template>
  <div>
    <TodoInput @addTodoItem="addTodoItem"/>
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
    TodoItem
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    addTodoItem(text) {
      this.todos.push(text);
    }
  }
};
</script>