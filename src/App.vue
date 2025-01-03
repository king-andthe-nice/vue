<script setup>
import { ref } from 'vue'
import axios from 'axios'

const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || 'https://h0t5na85db.hzh.sealos.run'

   getList()

const value = ref('')
const list = ref([])

async function getList() {
 const response = await axios({
    method: 'GET',
    url: `${API_BASE_URL}/get`,
  })
  list.value = response.data.list
  //console.log(response)
}
async function addList() {
 const response = await axios({
    method: 'POST',
    url: `${API_BASE_URL}/add`,
    data: {
      value: value.value,
      isCompleted: false,
      }, 
  })
  getList()
  value.value = ''
}
async function updateList(id) {
 const response = await axios({
    method: 'POST',
    url: `${API_BASE_URL}/update`,
    data: {
        id,
      }, 
  })
  getList()
}

async function delList(id) {
 const response = await axios({
    method: 'POST',
    url: `${API_BASE_URL}/delete`,
    data: {
        id,
      }, 
  })
  getList()
}

  // console.log(value.value)
  // console.log(list.value)

  console.log(1==="1")
  console.log(2==='2')
  console.log(3=="3")
  console.log(4=='4')


function add() {
  list.value.push({
    value: value.value,
    isCompleted: false,
  })

  value.value = ''
}

function del(index) {
  list.value.splice(index, 1)
}
</script>

<template>
  <div class="todo-app">
    <div class="title">Todo App</div>
    <div class="todo-form">
      <input
        v-model="value"
        type="text"
        class="todo-input"
        placeholder="Add a todo"
      />
      <div @click="addList"  class="todo-button">Add Todo</div>
  </div>

<div
  v-for="(item, index) in list"
  :key="item.id" 
  :class="[item.isCompleted ? 'completed' : 'item']"
>
  <div>
    <input @click="updateList(item._id)" v-model="item.isCompleted" type="checkbox" />
    <span class="name">{{ item.value }}</span>
  </div>
  <div @click="delList(item._id)" class="del">del</div>
</div>

  </div>
</template>


<style scoped>
.todo-app {
  box-sizing: border-box;
  margin-top: 40px;
  margin-left: 1%;
  padding-top: 30px;
  width: 98%;
  height: 500px;
  background: #ffffff;
  border-radius: 5px;
}

.title {
  text-align: center;
  font-size: 30px;
  font-weight: 700;
}

.todo-form {
  display: flex;
  margin: 20px 0 30px 20px;
}

.todo-button {
  width: 100px;
  height: 52px;
  border-radius: 0 20px 20px 0;

  text-align: center;
  background: linear-gradient(
    to right,
    rgb(113, 65, 168),
    rgba(44, 114, 251, 1)
  );
  color: #fff;
  line-height: 52px;
  cursor: pointer;
  font-size: 14px;
  user-select: none;
}

.todo-input {
  padding: 0px 15px 0px 15px;
  border-radius: 20px 0 0 20px;
  border: 1px solid #dfe1e5;
  outline: none;
  width: 60%;
  height: 50px;
}

.item {
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 20px;
}

.del {
  color: red;
}

.completed {
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 20px;
  text-decoration: line-through;
  opacity: 0.4;
}
</style>

<!-- <script setup>
import mybutton from './components/button.vue'


function add(test) {
  console.log(test)  
}
</script>

<template>
   <mybutton @ok="add" text="add"></mybutton>
   <mybutton text="hello" @click="add(123)" ></mybutton>
   <mybutton text="ni心" @click="add('ni心')" > </mybutton>
</template>

<style scoped>

</style> -->

