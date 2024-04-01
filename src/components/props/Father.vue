<script setup>
import { ref } from "vue";
import Son from "./Son.vue";

const username = ref("小圆");
</script>

<template>
  <Son :init="username"/>
</template>
