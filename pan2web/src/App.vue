<template>
  <div>
    <div id="header">
      <nav id="menu">
        <ul>
          <li @click="fbConnect">
            <div id="facebookImg" :style="fbImg(fbStatus.isLogin)"></div>
          </li>
          <li>
            <router-link tag="li" to="/Home">pan2web</router-link>
          </li>
          <li>
            <router-link tag="li" to="/TodoList">代辦事項</router-link>
          </li>
          <li>
            <router-link tag="li" to="/WorkOutNote">鍛鍊紀錄</router-link>
          </li>
        </ul>
      </nav>
    </div>
    <div id="content">
      <router-view/>
    </div>
  </div>
</template>

<script>
import VueRouter from "vue-router";
import TodoList from "./components/TodoList.vue";
import Home from "./components/Home.vue";
import WorkOutNote from "./components/WorkOutNote.vue";
export default {
  router: new VueRouter({
    routes: [
      { path: "/TodoList", component: TodoList },
      { path: "/Home", component: Home },
      { path: "/WorkOutNote", component: WorkOutNote }
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
body {
  background-image: url("./assets/bears.jpg");
  background-size: 100%;
  font-family: Microsoft JhengHei;
}
#header {
  position: fixed;
  width: 100vw;
  height: 7vh;
  /* background-color: rgba(80, 82, 81, 0.63); */
}
#menu {
  max-width: 70%;
  margin: 0 auto;
}
#menu ul {
  list-style: none;
}
#facebookImg {
  width: 40px;
  height: 40px;
  background-image: url("./assets/F_icon.svg");
  background-size: 100%;
}
#menu ul li {
  position: relative;
  float: left;
  color: rgba(0, 0, 0, 0.637);
  font-size: 140%;
  width: 11vw;
  float: left;
  text-align: center;
}
#content {
  position: relative;
  max-width: 70%;
  margin: 0 auto;
  top: 13vh;
}
</style>
