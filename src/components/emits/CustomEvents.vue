<script setup>
import CustomSubComponent from "./CustomSubComponent.vue";
import { ref } from "vue";
const number = ref(10);
const fun = val => {
  console.log(val);
  number.value += val;
};
</script>


<template>
  <p>{{number}}</p>
  <!-- 监听自定义事件 -->
  <CustomSubComponent @updateCount="fun" />
</template>

