<template lang="">
    <div>
        <header class="card">
    <h1>لیست وظایف </h1>
    
    <button id="theme-switcher" @click="changeTheme">
      <img v-if="defaultTheme =='darck'" src="../assets/icon-sun.svg" alt="Change color theme" />
      <img v-else src="../assets/icon-moon.svg" alt="Change color theme" />
    </button>
  </header>
    </div>
</template>
<script setup>
import { ref } from "vue";

const defaultTheme = ref("darck")
function changeTheme() {
  if (defaultTheme.value == "darck") {
    defaultTheme.value = "light";
    document.querySelector("body").classList.add("light");
  } else {
    defaultTheme.value = "darck";
    document.querySelector("body").classList.remove("light")
  }
}
</script>
<style lang="">

</style>