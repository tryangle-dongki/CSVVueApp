﻿<template>
  <button @click="downloadFile">ダウンロード</button>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
const apiBaseUrl = import.meta.env.VITE_API_BASE_URL;
const props = defineProps({
  fileName: {
    type: String,
    required: true
  }
})

// サーバーから処理されたCSVファイルをダウンロードする
async function downloadFile() {
  const fileName = props.fileName

  console.log('fileName:', fileName);

  const response = await fetch(`${apiBaseUrl}/api/File/download/${fileName}`, {
    method: 'GET'
  })

  if (!response.ok) {
    alert('Download failed.')
    return
  }

  const blob = await response.blob()
  const url = window.URL.createObjectURL(blob)

  const a = document.createElement('a')
  a.href = url
  a.download = fileName
  document.body.appendChild(a)
  a.click()
  window.URL.revokeObjectURL(url)
  document.body.removeChild(a)
}
</script>
