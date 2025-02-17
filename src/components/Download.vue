<template>
  <button @click="downloadFile">ダウンロード</button>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'

const props = defineProps({
  fileName: {
    type: String,
    required: true
  }
})

// 서버에서 처리된 CSV 파일 다운로드
async function downloadFile() {
  const fileName = props.fileName

  console.log('fileName:', fileName);

  const response = await fetch(`https://csv-handler-app-erhrhfh6hfecbdaf.japaneast-01.azurewebsites.net/api/File/download/${fileName}`, {
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
