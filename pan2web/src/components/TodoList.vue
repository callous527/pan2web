<template>
  <div>
    <TodoInput @addTodoItem="addTodoItem"/>
    <ul>
      <TodoItem
        v-for="(todo,index) in todos"
        :data="todo"
        :key="index"
        @click.native="deleteTodoItem(index)"
      />
    </ul>
  </div>
</template>
<script>
import TodoInput from "./TodoInput.vue";
import TodoItem from "./TodoItem.vue";

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
    },
    deleteTodoItem(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>
