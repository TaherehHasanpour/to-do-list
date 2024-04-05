<template >
    <div>
        <div class="card add">
      <div class="cb-container">
        <button id="add-btn" @click="AddTodo">+</button>
      </div>
      <div class="txt-container">
        <label for="addt">افزودن </label>
        <input v-model="todoTitle" @keypress.enter="AddTodo" type="text" class="txt-input" placeholder="افزودن وظیفه جدید..." spellcheck="false" autocomplete="off"
          id="addt" dir="rtl" />
      </div>
    </div>
    </div>
</template>
<script setup>
import { ref,defineEmits } from "vue";

const todoTitle=ref("");

const emits = defineEmits(["AddNewTodo"]);
function AddTodo(){
  emits("AddNewTodo",todoTitle.value);
  todoTitle.value="";
}
</script>
<style lang="">
    
</style>