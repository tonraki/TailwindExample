

<template>
  <h2>Two-Way Binding</h2>
  <input v-model="message" /> <!-- v-model ทำให้ UI และตัวแปรซิงค์กัน -->
  <p>ค่าปัจจุบัน: {{ message }}</p>
</template>

<script setup>
import { ref } from 'vue'

const message = ref("Hello from Nuxt!")
</script>
