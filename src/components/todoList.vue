<script setup>
import { ref, reactive } from "vue";
let todos = ref([{ id: 0, msg: "上课" }]);
let taskText = ref("");
let nextId = ref("");
function addTask() {
  if (taskText.value.length == 0) {
    alert("请输入任务");
    return;
  } else {
    nextId.value = Math.max(...todos.value.map((item) => item.id)) + 1;
    var obj = {
      id: nextId.value,
      msg: taskText.value,
    };
    todos.value.push(obj);
    console.log(todos.value);
    taskText = ref("");
  }
}
function removeTask(id) {
  todos.value = todos.value.filter((item) => item.id !== id);
}
</script>
<template>
  <div>
    <form action="" @submit.prevent="addTask">
      <input type="text" placeholder="请输入..." v-model="taskText" />
      <button>提交</button>
    </form>
    <ul v-for="item in todos" :key="item.id">
      {{
        item.msg
      }}
      <button @click="removeTask(item.id)">删除</button>
      <hr />
    </ul>
  </div>
</template>