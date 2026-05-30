<script setup>
import { ref } from 'vue'
import ComingSoon from './components/ComingSoon.vue'

const base = import.meta.env.BASE_URL
const images = Array.from({ length: 5 }, (_, i) => `${base}${i + 1}.jpg`)

const altTexts = [
  'UNO 大賽 x XS 能量飲料',
  'XS 能量飲料系列介紹',
  'XS 的故事',
  'XS 全口味介紹',
  '活動辦法',
]

// const signupUrl =
//   'https://docs.google.com/forms/d/e/1FAIpQLSeDzGj9mdnR_P8A7BJplJ8mSK6aIkLHxkqp4-_J7eZuwE0ACQ/viewform'

// 開發者模式：設為 true 時顯示「暫無此頁面」佔位頁
const isDev = import.meta.env.DEV
const devMode = ref(false)
</script>

<template>
  <!-- 開發者模式切換按鈕 -->
  <button
    v-if="isDev"
    class="fixed top-3 right-3 z-50 w-10 h-10 rounded-full shadow-lg flex items-center justify-center text-xs font-bold transition-all duration-300 cursor-pointer"
    :class="devMode ? 'bg-amber-500 text-white' : 'bg-gray-800/60 text-white/80 backdrop-blur-sm'"
    :title="devMode ? '返回正常頁面' : '切換開發者模式（顯示佔位頁）'"
    @click="devMode = !devMode"
  >
    {{ devMode ? '✕' : 'DEV' }}
  </button>

  <!-- 佔位頁面 -->
  <ComingSoon v-if="devMode" />

  <!-- 正常頁面內容 -->
  <div v-else class="flex flex-col">
    <a
      v-for="(src, index) in images"
      :key="index"
      target="_blank"
      rel="noopener"
      class="block"
    >
      <img :src="src" :alt="altTexts[index]" class="w-full block" />
    </a>
  </div>
</template>
