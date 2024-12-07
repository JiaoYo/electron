<template>
  <h1>
    {{ message }}
  </h1>
  <button style="-webkit-app-region: no-drag;" @click="sentMessage" >发送信息</button>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
const router = useRouter()
const message = ref('')
const sentMessage = async () => {
  message.value = await window.ipcRenderer.invoke('post-message')
}
</script>

<style scoped></style>
<style scoped lang="less">
.box {
  width: 300px;
  height: 300px;
}
</style>
