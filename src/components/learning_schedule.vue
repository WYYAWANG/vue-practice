<script setup>
import { ref } from "vue";
let subject = ref("");
let content = ref("");
let nextId = ref("");
let selectedOption = ref("自习室");
let options = ref([
  { placeCode: 0, place: "自习室" },
  { placeCode: 1, place: "图书馆" },
  { placeCode: 2, place: "宿舍" },
]);
const list = ref([
  {
    id: "1",
    subject: "Vue.js前端实战开发",
    content: "学习指令，例如 v-if、v-for、v-model 等",
    place: "自习室",
    status: false,
  },
]);
function remove(id, status) {
  //filter函数
  if (status) {
    list.value = list.value.filter((item) => item.id !== id);
  } else {
    alert("请先完成学习计划后再进行删除操作");
  }
}
function add() {
  if (subject.value == "") {
    alert("学习科目为必填项");
    return;
  }
  //要提前讲解:展开运算符（取最大数Math.max(...[14,3,77,30])）
  //map() 方法创建一个新数组，这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成
  nextId.value = Math.max(...list.value.map((item) => item.id)) + 1;
  console.log(selectedOption.value);
  const obj = {
    id: nextId.value,
    subject: subject.value,
    content: content.value,
    place: selectedOption.value,
    status: false,
  };
  list.value.push(obj);
  subject.value = "";
  content.value = "";
  selectedOption.value = "自习室";
}
</script>

<template>
  <div class="card">
    <div class="card-header">学习计划表</div>
    <div class="card-body">
      <form action="" @submit.prevent="add">
        <div class="row">
          <div class="col-auto">
            <div class="input-group mb-3">
              <span class="input-group-text" id="basic-addon1">学习科目</span>
              <input
                type="text"
                class="form-control"
                placeholder="请输入学习科目"
                v-model.trim="subject"
              />
            </div>
          </div>
          <div class="col-auto">
            <div class="input-group">
              <span class="input-group-text">学习内容</span>
              <textarea
                class="form-control"
                aria-label="With textarea"
                v-model.trim="content"
                :style="{ height: '32px' }"
              ></textarea>
            </div>
          </div>
          <div class="col-auto">
            <div class="input-group mb-3">
              <label class="input-group-text" for="inputGroupSelect01"
                >学习地点</label
              >
              <select
                class="form-select"
                id="inputGroupSelect01"
                v-model="selectedOption"
              >
                <option
                  v-for="option in options"
                  :key="option.placeCode"
                  :value="option.place"
                >
                  {{ option.place }}
                </option>
              </select>
            </div>
          </div>
          <div class="col-auto">
            <button type="submit" class="btn btn-primary">添加</button>
          </div>
        </div>
      </form>
    </div>
  </div>
  <table class="table table-success table-striped table-hover table-bordered">
    <thead>
      <tr>
        <th scope="col">序号</th>
        <th scope="col">学习科目</th>
        <th scope="col">学习内容</th>
        <th scope="col">学习地点</th>
        <th scope="col">完成状态</th>
        <th scope="col">操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in list" :key="item.id">
        <th scope="row">{{ item.id }}</th>
        <td>{{ item.subject }}</td>
        <td>{{ item.content }}</td>
        <td>{{ item.place }}</td>
        <td>
          <div class="form-check form-switch">
            <input
              class="form-check-input"
              type="checkbox"
              role="switch"
              :id="'cb' + item.id"
              checked
              v-model="item.status"
            />
            <label
              class="form-check-label"
              :for="'cb' + item.id"
              v-if="item.status"
              >已完成</label
            >
            <label class="form-check-label" :for="'cb' + item.id" v-else
              >未完成</label
            >
          </div>
        </td>
        <td>
          <a href="javascript:;" @click="remove(item.id, item.status)">删除</a>
        </td>
      </tr>
    </tbody>
  </table>
</template>