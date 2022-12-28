<template>
  <router-view />
</template>

<script lang="ts">
import { ref, provide } from "vue";
import { router } from "./router";

export default {
  name: "App",
  setup() {
    //获取视口宽度
    const width = document.documentElement.clientWidth;
    //定义一个其他组件可以访问的变量 用来控制aside的显示
    const asideVisible = ref(width <= 500 ? false : true);
    //把变量传出去
    provide("asideVisible", asideVisible);
    //在每次路由变化后
    router.afterEach(() => {
      if (width <= 500) {
        asideVisible.value = false;
      }
    });
  },
};
</script>
