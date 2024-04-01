<template>
  初始值为：{{ num }}
  姓名：{{ init }}
</template>
<script setup>
import { ref } from 'vue';
// 声明props
const props = defineProps({
  num: { type: Number, required: false, default: 9 },
  init: {
    type: [Number,String],
    validator(val) {
      console.log("val:" + val);
      //返回值为：true则验证通过，false为验证不通过
      return [""].indexOf(val) !== -1; //自定义验证函数
    }
  }
});
// console.log(props);
</script>