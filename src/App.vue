<template>
  <div>
    <TestComponent/>
<!--    <Btn :plusBtnProps="plusBtnProps"/>-->
    <Btn :severity="plusBtnProps.severity"
         :icon="plusBtnProps.icon"
         :raised="plusBtnProps.raised"
         :rounded="plusBtnProps.rounded"
    />
    <Btn :severity="minusBtnProps.severity"
         :icon="minusBtnProps.icon"
         :raised="minusBtnProps.raised"
         :rounded="minusBtnProps.rounded"
    />
    <br><br><br>
    <Home/>

  </div>

</template>

<script setup>
import TestComponent from "./components/TestComponent.vue";
import Btn from "./components/Btn.vue"
import Home from "./components/Home.vue"
import {ref} from "vue";

const plusBtnProps = {
  severity: "Primary",
  icon: "pi pi-plus",
  raised: true,
  rounded: true
}
const minusBtnProps = {
  severity: "Primary",
  icon: "pi pi-minus",
  raised: true,
  rounded: true
}

</script>

<style scoped>





</style>
