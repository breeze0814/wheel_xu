<template>
  <div>
    <Topnav />
    <div class="logo"></div>
    <div class="menu"></div>
    <div class="content">
      <aside>侧边栏</aside>
      <main>主内容</main>
    </div>
  </div>
</template>
<script lang="ts">
import Topnav from "../components/Topnav.vue";
export default {
  components: { Topnav },
};
</script>
