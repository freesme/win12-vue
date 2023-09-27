<script setup>
import {ref} from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <div class="box">

  </div>
</template>

<style scoped>
.box {
  background: #e8e7e7;
  width: 1000px;
  height: 500px;
  align-items: center;
  display: flex;
  justify-content: center;
}


</style>
