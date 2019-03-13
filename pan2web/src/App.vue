<template>
  <div>
    <div>
      <nav>
        <ul>
          <li @click="fbConnect">
            <div id="facebookImg" :style="fbImg(fbStatus.isLogin)"></div>
          </li>
          <li>
            <router-link to="/Home">Home</router-link>
          </li>
          <li>
            <router-link to="/TodoList">TodoList</router-link>
          </li>
        </ul>
      </nav>
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
  data() {
    return {
      fbStatus: { isLogin: false, id: "" }
    };
  },
  methods: {
    fbConnect() {
      FB.login(this.fbStatusGet);
    },
    fbStatusGet(result) {
      this.$set(this.fbStatus, "isLogin", result.status === "connected");
      FB.api("/me", rs => {
        this.$set(this.fbStatus, "id", rs.id);
      });
    },
    fbImg(isLogin) {
      if (isLogin) return {};
      else
        return {
          filter: "grayscale(100%)"
        };
    }
  },
  mounted() {
    FB.init({
      appId: 2226921694190612,
      version: "v3.2"
    });
    FB.getLoginStatus(this.fbStatusGet);
  }
};
</script>
<style>
#facebookImg {
  width: 50px;
  height: 50px;
  background-image: url("./assets/F_icon.svg");
  background-size: 100%;
}
</style>
