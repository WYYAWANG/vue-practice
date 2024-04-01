<template>
  <div>子组件</div>
  <hr />
  从爷爷组件收到的资金：{{ money1 }}
  <button @click="updateMoney1(100)">单击增加资金</button>
</template>

<script setup>
import { inject } from "vue";
let money1 = inject("money");
let updateMoney1 = inject("updateMoney");

const foo = inject("foo", "默认值");
//默认值是工厂函数
const baz = inject("foo", () => ({name: 'bar' }),true);
//默认值是函数
const fn = inject("function", () => {console.log('hi')}, false);
console.log('foo:'+foo);
console.log('baz:'+baz.name);
fn()
</script>