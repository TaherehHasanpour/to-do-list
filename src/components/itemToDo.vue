<template >
    <div>
        <li class="card" draggable="true">
        <div class="cb-container">
          <input type="checkbox" class="cb-input" :checked="todo.isCompleted" @click="changeStatus" />
          <span class="check"></span>
        </div>
        <p class="item"> 
          <del v-if="todo.isComplete">  {{todo.title}} </del>
        <span v-else> {{todo.title}}</span>
        </p>
        <button class="clear" @click="deleteTodo">
          <img src="../assets/icon-cross.svg" alt="Clear it" />
        </button>
      </li>
    </div>
</template>
<script setup>
import { defineProps,toRef,defineEmits} from "vue";
const props = defineProps({
  todo: Object,
})
const todo = toRef(props, "todo");
const emits = defineEmits(["deleteTodo ,chengStatus"]);

function deleteTodo() {
  if(confirm("آیا از حذف اطمینان دارید"))
  emits("deleteTodo", todo.value.id);
}
function changeStatus() {
  emits("changeStatus", todo.value.id, !(todo.value.isComplete));
}
</script>
<style lang="">
    
</style>