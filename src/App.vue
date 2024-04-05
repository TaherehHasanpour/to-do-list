<template>
  <div>
    <appHeader></appHeader>
    <main>
      <addToDo @AddNewTodo="addToDoitem"></addToDo>
      <ul class="todos">
        <template v-for="(item, i) in tabstatus" :key="item.id">
          <itemToDo :todo="item" @deleteTodo="deleteTodo" @changeStatus="changeTodoStatus" @dragover.prevent
            @dragstart="dragStart(i)" @drop="drop(i)"></itemToDo>
        </template>
      </ul>
      <div class="card stat">
        <p class="corner"><span id="items-left">{{ getActiveTodoCount }}</span> مورد باقی مانده</p>
        <div class="filter">
          <button id="all" :class="{ on: activeTab == 'all' }" @click="changeTodo('all')">همه</button>
          <button id="active" :class="{ on: activeTab == 'active' }" @click="changeTodo('active')">فعال</button>
          <button id="completed" :class="{ on: activeTab == 'completed' }"
            @click="changeTodo('completed')">تکمیل</button>
        </div>
        <div class="corner">
          <button id="clear-completed" @click="deletIsCompleted">حذف تکمیل شده ها</button>
        </div>
      </div>
    </main>
    <appFooter></appFooter>
  </div>
</template>
<script setup>
import appHeader from './components/appHeader.vue';
import appFooter from './components/appFooter.vue';
import addToDo from './components/addToDo.vue';
import itemToDo from './components/itemToDo.vue';
import { ref, computed } from 'vue';
import { useToast } from "vue-toastification";
const todos = ref([]);
const draging = ref(-1);
const activeTab = ref("all");
const toast = useToast();
const tabstatus = computed(() => {
  switch (activeTab.value) {
    case "all": {
      return todos.value;
    }
    case "active": {
      return todos.value.filter((f) => f.isComplete == false);
    }
    case "completed": {
      return todos.value.filter((f) => f.isComplete == true);
    }
  }
});
const getActiveTodoCount = computed(() => {
  return todos.value.filter((f) => f.isComplete === false).length;
});

function addToDoitem(todoTitle) {
  if (!todoTitle) {
    toast.error("عنوان را وارد کنید");
    return;
  }
  var id = Math.random().toString(16).slice(2);
  todos.value.push({
    id: id,
    title: todoTitle,
    isComplete: false
  });
  toast.success("عملیات با موفقیت انجام شد");
};
function deleteTodo(id) {
  todos.value = todos.value.filter(f => f.id !== id)
}
function changeTodoStatus(id, newStatus) {
  var newTodos = [...todos.value];
  var selectedTodo = newTodos.find((f) => f.id === id);
  selectedTodo.isComplete = newStatus;
  todos.value = newTodos;
}
function deletIsCompleted() {
  if (confirm("آیا از انجام عملیات اطمینان دارید ؟")) {
    var newTodos = [...todos.value];
    newTodos = newTodos.filter((f) => f.isComplete === false);
    todos.value = newTodos;
    
  toast.error();("عملیات با موفقیت انجام شد");
  }
}
function dragStart(index) {
  draging.value = index
}
function drop(index) {
  var newElement = todos.value.splice(draging.value, 1)[0];
  todos.value.splice(index, 0, newElement);
};
function changeTodo(nameTab) {
  activeTab.value = nameTab;
}

</script>

<style scoped></style>
