<script setup lang="ts">
import { onMounted, ref } from "vue";

// left左侧偏移量
const offset = ref(0);
// 菜单宽度
const width = ref(0);
// 激活菜单
const active = ref(3);
// 模拟菜单列表数据
const menus = ref<string[]>([
  "首页",
  "集团介绍",
  "万科资讯",
  "多元业务",
  "投资这关系",
  "超极无敌长的数据菜单舒适",
  "社会责任",
  "加入万科",
  "About me",
  "投诉建议",
]);

// 鼠标移入事件
const mouseenterHandler = (e: MouseEvent) => {
  const el = e.target as HTMLLIElement;
  offset.value = el.getBoundingClientRect().left;
  width.value = el.getBoundingClientRect().width;
};

// 鼠标移除事件
const mouseleaveHandler = () => {
  initMenuActiveStyle();
};

// 初始化菜单选中样式
const initMenuActiveStyle = () => {
  const activeEl = document.getElementsByClassName("active");
  offset.value = activeEl[0]?.getBoundingClientRect().left;
  width.value = activeEl[0]?.getBoundingClientRect().width;
};

// 触发一次选中当前激活菜单
onMounted(() => {
  initMenuActiveStyle();
});
</script>

<template>
  <div class="relative">
    <ul
      class="flex justify-start items-center bg-slate-400/20"
      @mouseleave="mouseleaveHandler"
    >
      <li
        class="px-4 py-6 cursor-pointer"
        :class="active === index ? 'active' : ''"
        v-for="(item, index) in menus"
        :key="item"
        @mouseenter="mouseenterHandler"
      >
        {{ item }}
      </li>
    </ul>
    <div
      class="h-1 absolute bottom-0 bg-blue-500 w-16 duration-300 ease-in-out"
      :style="{ left: offset + 'px', width: width + 'px' }"
    ></div>
  </div>
</template>

<style scoped></style>
