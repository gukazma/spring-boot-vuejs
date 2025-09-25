<template>
  <button class="Search__button" @click="callRestService">
    CALL Spring Boot REST backend service
  </button>

  <h3>{{ responseMessage }}</h3>

  <!-- 可选：显示错误信息 -->
  <!-- <div v-if="errors.length" class="error">
    <p v-for="(error, index) in errors" :key="index">
      Error: {{ error.message || error }}
    </p>
  </div> -->
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

// 响应式状态
const responseMessage = ref('')
const errors = ref([])

// 方法：调用 REST 服务
const callRestService = async () => {
  errors.value = [] // 清空之前的错误
  try {
    const response = await axios.get('hello')
    responseMessage.value = response.data // 自动响应式更新
  } catch (e) {
    errors.value.push(e)
    console.error('请求失败:', e)
  }
}
</script>

<style scoped>
.Search__button {
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.Search__button:hover {
  background-color: #0056b3;
}

.error {
  color: red;
  margin-top: 16px;
}
</style>