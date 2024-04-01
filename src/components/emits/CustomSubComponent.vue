<script setup>
import { ref } from "vue";
//defineEmits声明自定义事件
const emit2 = defineEmits(["updateCount"]);
const count = ref(1);
//定义方法来触发自定义事件,传输数据
const add = () => {
  count.value++;
  emit2("updateCount", 2);
};
</script>

<template>
  <p>count的值为：{{ count }}</p>
  <button @click="add">+1</button>
  <!-- 内联事件处理器，调用$emit方法触发 -->
  <button @click="$emit('updateCount',3)">父亲+3</button>
</template>