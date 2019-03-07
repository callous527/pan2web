<template>
  <div>
    <div class="menu">
      <router-link to="/TodoList">TodoList</router-link>
    </div>
    <div>
      <router-view/>
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import VueRouter from "vue-router";

export default {
  router: new VueRouter({
    routes: [
      { path: "/TodoList", component: TodoList },
    ]
  }),
  components: {
    TodoList
  }
};
</script>