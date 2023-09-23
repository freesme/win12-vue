<template>
  <ProgressBar :progress="progress" :load-time=1000 backColor="#C81D1DFF" :manual="false"/>
  <button style="width: 100px" @click=addProgress>STEP</button>
</template>


<script setup>
import ProgressBar from "./components/ProgressBar.vue";
import {ref, onMounted} from "vue";
const progress = ref(90);
function addProgress() {!
  console.log(progress.value)
  progress.value++
}

</script>

<style scoped>

</style>
