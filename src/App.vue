<script setup lang="ts">
import { ref, onMounted } from 'vue'
const handleMinWin = () => {
  window?.ipcRenderer.send('minimize')
  isImize()
}
const handleClose = () => {
  window?.ipcRenderer.send('close')
}
const handleMaxWin = () => {
  window?.ipcRenderer.send('maximize')
  isImize()
}
const isiminimize = ref(false)
const isImize = async () => {
  isiminimize.value = await window?.ipcRenderer.invoke('isimize')
}
onMounted(() => {
  isImize()
})
const iconName = ref('')
</script>

<template>
  <div class="app">
    <header>
      <div class="close">
        <span class="icon" @click="handleMinWin">
          <svg  width="200px" height="200.00px" viewBox="0 0 1024 1024" version="1.1"
            xmlns="http://www.w3.org/2000/svg">
            <path
              d="M853.333333 554.666667H170.666667c-23.466667 0-42.666667-19.2-42.666667-42.666667s19.2-42.666667 42.666667-42.666667h682.666666c23.466667 0 42.666667 19.2 42.666667 42.666667s-19.2 42.666667-42.666667 42.666667z"
              fill="#666666" />
          </svg>
        </span>
        <span class="icon" @click="handleMaxWin" v-if="!isiminimize">
          <svg  width="160px" height="160.00px" viewBox="0 0 1024 1024" version="1.1"
            xmlns="http://www.w3.org/2000/svg">
            <path
              d="M800 928H224c-70.692 0-128-57.308-128-128V224c0-70.692 57.308-128 128-128h576c70.692 0 128 57.308 128 128v576c0 70.692-57.308 128-128 128z m64-704c0-35.346-28.654-64-64-64H224c-35.346 0-64 28.654-64 64v576c0 35.346 28.654 64 64 64h576c35.346 0 64-28.654 64-64V224z"
              fill="#666666" />
          </svg>
        </span>
        <span class="icon" @click="handleMaxWin" v-else>
          <svg  width="160px" height="160.00px" viewBox="0 0 1024 1024" version="1.1"
            xmlns="http://www.w3.org/2000/svg">
            <path
              d="M741.9 281.7v663h-663v-663h663m0.8-76.1H78.1c-41.3 0-76.1 34-76.1 76.1v664.6c0 41.3 34 76.1 76.1 76.1h664.6c41.3 0 76.1-34 76.1-76.1V280.9c-0.8-42.1-34-75.3-76.1-75.3z m204.8-204H281.3c-41.3 0-74.5 34-75.3 74.5v77.7h76.1V77.7h663v663H869v76.1h77.7c41.3 0 74.5-34 75.3-75.3V76.1c0-40.5-34-74.5-74.5-74.5z"
              fill="#666666" />
          </svg>
        </span>
        <span class="icon closeicon" @click="handleClose">
          <svg  width="200px" height="200.00px" viewBox="0 0 1024 1024" version="1.1"
            xmlns="http://www.w3.org/2000/svg">
            <path
              d="M571.733333 512l268.8-268.8c17.066667-17.066667 17.066667-42.666667 0-59.733333-17.066667-17.066667-42.666667-17.066667-59.733333 0L512 452.266667 243.2 183.466667c-17.066667-17.066667-42.666667-17.066667-59.733333 0-17.066667 17.066667-17.066667 42.666667 0 59.733333L452.266667 512 183.466667 780.8c-17.066667 17.066667-17.066667 42.666667 0 59.733333 8.533333 8.533333 19.2 12.8 29.866666 12.8s21.333333-4.266667 29.866667-12.8L512 571.733333l268.8 268.8c8.533333 8.533333 19.2 12.8 29.866667 12.8s21.333333-4.266667 29.866666-12.8c17.066667-17.066667 17.066667-42.666667 0-59.733333L571.733333 512z"
              fill="#666666" />
          </svg>
        </span>
      </div>
    </header>
    <router-view></router-view>
  </div>
</template>

<style scoped lang="scss">
.app {
  padding-top: 50px;
}

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  -webkit-app-region: drag;
  background-color: #dde3e9;
}

.close {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 40px;
  color: #333;
  border-radius: 5px;
  cursor: pointer;
  overflow: hidden;
  float: right;
}

.icon {
  width: 40px;
  height: 40px;
  -webkit-app-region: no-drag;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon svg {
  width: 20px;
  height: 20px;
}

.icon.closeicon:hover {
  background-color: #f00 !important;

  path {
    fill: #fff !important;
  }
}

.icon:hover {
  background-color: #ccc;

  path {
    fill: #333 !important;
  }
}
</style>