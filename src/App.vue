<template>
<!--  <ProgressBar :progress="progress" :load-time=1000 backColor="#C81D1DFF" :manual="false" :on-progress-complete="hel"/>-->
<!--  <button style="width: 100px" @click=addProgress>STEP</button>-->
<!--  <Panel></Panel>-->
  <application></application>
</template>


<script setup>
import {ref} from "vue";
import Application from "./components/App/Application.vue";

const progress = ref(90);

function addProgress() {
  progress.value++
}


async function hel() {
  window.alert("Hel!")
  return "hel"
}

</script>

<style scoped>

</style>
