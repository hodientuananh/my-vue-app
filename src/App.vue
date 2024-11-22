<script setup>
import { ref } from "vue";

const items = ref([{ message: "First" }, { message: "Second" }]);
const newItem = ref("");

function addItem() {
  items.value.push({ message: newItem.value });
  newItem.value = "";
}
function deleteItem(item) {
  items.value = items.value.filter((i) => i !== item);
}
function editItem(item) {
  newItem.value = item.message;
  deleteItem(item);
}
function toggleDone(item) {
  item.done = !item.done;
}
</script>

<template>
  <div class="container">
    <h1>To do list</h1>
    <div class="input-group input-group-lg mb-3">
      <span class="input-group-text" id="inputGroup-sizing-sm"
        >Add new item</span
      >
      <input
        type="text"
        class="form-control"
        aria-label="Sizing example input"
        aria-describedby="inputGroup-sizing-lg"
        v-model="newItem"
        @keyup.enter="addItem"
      />
    </div>
    <ul class="list-group" v-for="item in items" :key="item.message">
      <li class="list-group-item" :class="{'done': item.done}">
        {{ item.message }}
        <div
          class="btn-group float-end"
          role="group"
          aria-label="Basic mixed styles example"
        >
            <button type="button" class="btn btn-success" @click="toggleDone(item)">Done</button>
          <button type="button" class="btn btn-warning" @click="editItem(item)">Edit</button>
          <button type="button" class="btn btn-danger" @click="deleteItem(item)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
