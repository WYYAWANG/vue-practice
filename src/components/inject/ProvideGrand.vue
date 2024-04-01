<template>
    <div>爷爷组件</div>
    <hr>
    <ProvideParent/>
</template>

<script setup>
import ProvideParent from './ProvideParent.vue'
import { provide, ref } from 'vue'
let money = ref(100)
let updateMoney = (val) => {
    money.value += val
}
provide('money',money)
provide('updateMoney',updateMoney)

</script>