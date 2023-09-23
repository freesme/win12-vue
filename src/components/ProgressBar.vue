<template>
  <div>
    <div class="layout">
      <p style="margin-right: 6px">{{ title }}</p>
      <div class="progress-container font-doc" :style="{width: width + 'px', background: backColor}">
        <div class="progress-bar" :style="{ width: progressInner +'%', background: activeColor}"></div>
      </div>
      <p style="width:20px; margin-left: 5px"> {{ progressInner }}% </p>
    </div>
    <p style="text-align: center; margin-top: -18px">{{ info }}</p>
  </div>
</template>

<script setup>
import {ref, toRefs, watch, onMounted} from 'vue';

const props = defineProps({
  title: {type: String, default: 'Starting'},
  info: {type: String, default: 'Press F2 or touch screen to enter SETUP'},
  width: {type: Number, default: 500},              // 进度条长度
  progress: {type: Number, default: 0},             // 初始进度%（百分比）
  manual: {type: Boolean, default: true},           // 手动调用
  loadTime: {type: Number, default: 1000},          // 加载时长
  backColor: {type: String, default: '#acabac'},    // 背景颜色
  activeColor: {type: String, default: '#2f2e2e'},  // 活动颜色

  onProgressComplete: {                             // 回调函数属性
    type: Function, default: () => {
      console.log("complete!")
    }
  },
})

const {title, info, width, progress, manual, loadTime, backColor, activeColor, onProgressComplete} = toRefs(props)
const progressInner = ref(0);

function loadProgress() {
  progressInner.value = progress.value
  if (!manual.value) {
    let timeout = loadTime.value / (100 - progress.value)
    const interval = setInterval(() => {
      progressInner.value++
      if (progressInner.value >= 100) {
        clearInterval(interval)
      }
    }, timeout);
  }
}

onMounted(() => {
  loadProgress()
})

watch(progressInner, (newVal) => {
  console.log("inner:", newVal)
  if (newVal === 100) {
    // function maybe Blocking page rendering
    setTimeout(() => props.onProgressComplete()
        .then(result => {
          console.log(result)
        }), 500)
  }
})


watch(progress, (newVal) => {
  console.log(newVal)
  progressInner.value = newVal < 100 ? progress.value : 100
})


</script>

<style>

* {
  font-family: doc, sans-serif;
}

.layout {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: -10px;
}

.progress-container {
  display: flex;
  height: 20px;
  background-color: #acabac;
  position: relative;
}

.progress-bar {
  height: 100%;
  background-color: #0074d9;
  transition: width 0.2s ease-in-out;
}

</style>
