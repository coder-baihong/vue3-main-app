<template>
  <div>
    登录页
    <div>用户名：<input v-model="username" /></div>
    <div>密码：<input v-model="password" /></div>
    <div><button @click="login">登录</button></div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import { useStore } from "vuex";
import { useRouter } from "vue-router";
import { actions } from "@/micros";

export default {
  setup() {
    const username = ref("");
    const password = ref("");
    const store = useStore();
    const router = useRouter();
    onMounted(() => {
      actions.onGlobalStateChange((state) => {
        // state: 变更后的状态; prevState: 变更前的状态
        console.log("主应用观察者：状态改变", state);
      });
    });

    const login = () => {
      if (username.value && password.value) {
        store.commit("setToken", "123456");
        actions.setGlobalState({
          globalToken: "123456"
        });
        router.push({
          path: "/"
        });
      }
    };

    return {
      username,
      password,
      login
    };
  }
};
</script>

<style lang="scss" scoped></style>
