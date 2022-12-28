<template>
  <router-view />
</template>

<script lang="ts">
import { ref, provide } from "vue";

export default {
  name: "App",
  setup() {
    //定义一个其他组件可以访问的变量 用来控制aside的显示
    const asideVisible = ref(false);
    //把变量传出去
    provide("asideVisible", asideVisible);
  },
};
</script>
