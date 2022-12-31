<template>
  <div>Tabs 示例</div>
  <H1>示例1</H1>
  <Tabs v-model:selected="x">
    <Tab title="导航111">内容1</Tab>
    <Tab title="导航2222222222222">内容2</Tab>
  </Tabs>
</template>
<script lang="ts">
import Tabs from "../lib/Tabs.vue";
import Tab from "../lib/Tab.vue";
import { ref } from "vue";
export default {
  components: { Tabs, Tab },

  setup(props) {
    const x = ref("导航111");
    return { x };
  },
};
</script>
