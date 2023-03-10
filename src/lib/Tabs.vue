<template>
  <div class="zoe-tabs">
    <div class="zoe-tabs-nav" ref="container">
      <div
        class="zoe-tabs-nav-item"
        v-for="(t, index) in titles"
        :ref="
          (el) => {
            if (t === selected) selectedItem = el;
          }
        "
        @click="select(t)"
        :class="{ selected: t === selected }"
        :key="index"
      >
        {{ t }}
      </div>
      <div class="zoe-tabs-nav-indicator" ref="indicator"></div>
    </div>
    <div class="zoe-tabs-content">
      <component
        :is="current"
        :key="current.props.title"
      />
    </div>
  </div>
</template>
<script lang="ts">
import { computed, ref, onMounted, onUpdated, watchEffect } from "vue";
import Tab from "./Tab.vue";
export default {
  props: {
    selected: {
      type: String,
    },
  },
  setup(props, context) {
    const selectedItem = ref(null);
    const indicator = ref<HTMLDivElement>(null);
    const container = ref<HTMLDivElement>(null);
    onMounted(() => {
      watchEffect(() => {
        console.log('1111');
        // 获取当前选中元素的宽度
        const { width } = selectedItem.value.getBoundingClientRect();
        indicator.value.style.width = width + "px";
        const { left: left1 } = selectedItem.value.getBoundingClientRect();
        const { left: left2 } = container.value.getBoundingClientRect();
        indicator.value.style.left = left1 - left2 + "px";
      },{flush:'post'});
    });
    const defaults = context.slots.default();
    defaults.forEach((tag) => {
      if (tag.type !== Tab) {
        throw new Error("Tabs 子标签必须是 Tab");
      }
    });
    const current = computed(() => {
      return defaults.find((tag) => tag.props.title === props.selected);
    });
    const titles = defaults.map((tag) => {
      return tag.props.title;
    });
    const select = (title: string) => {
      context.emit("update:selected", title);
    };
    return {
      defaults,
      titles,
      select,
      current,
      selectedItem,
      indicator,
      container,
    };
  },
};
</script>
<style lang="scss">
$blue: #40a9ff;
$color: #333;
$border-color: #d9d9d9;
.zoe-tabs {
  &-nav {
    display: flex;
    color: $color;
    border-bottom: 1px solid $border-color;
    position: relative;
    &-item {
      padding: 8px 0;
      margin: 0 16px;
      cursor: pointer;
      &:first-child {
        margin-left: 0;
      }
      &.selected {
        color: $blue;
      }
    }
    &-indicator {
      position: absolute;
      height: 3px;
      background: $blue;
      left: 0;
      bottom: -1px;
      transition: all 300ms;
    }
  }
  &-content {
    padding: 8px 0;
  }
}
</style>
