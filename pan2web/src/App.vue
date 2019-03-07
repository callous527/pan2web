<template>
  <div>
    <div class="menu">
      <router-link to="/Home">Home</router-link>
      <router-link to="/TodoList">TodoList</router-link>
    </div>
    <div>
      <router-view/>
    </div>
  </div>
</template>

<script>
import VueRouter from "vue-router";
import TodoList from "./components/TodoList.vue";
import Home from "./components/Home.vue";

export default {
  router: new VueRouter({
    routes: [
      { path: "/TodoList", component: TodoList },
      { path: "/Home", component: Home }
    ]
  }),
  components: {
    TodoList
  }
};
</script>