<template>
  <div>
    <h1>CSV ファイルアップロード</h1>
    <input type="file" @change="handleFileUpload" accept=".csv" />
    <button @click="uploadFile">アップロード</button>

    <div v-if="uploadStatus">
      <p>{{ uploadStatus }}</p>
      <DownloadButton v-if="uploadedFileName" :fileName="uploadedFileName" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import DownloadButton from './Download.vue' // ダウンロードボタンコンポーネントをインポート

const apiBaseUrl = import.meta.env.VITE_API_BASE_URL;
const file = ref<File | null>(null)
const uploadStatus = ref<string | null>(null)
const uploadedFileName = ref<string | null>(null)

// ファイル選択時の処理
function handleFileUpload(event: Event) {
  const input = event.target as HTMLInputElement
  if (input.files && input.files[0]) {
    file.value = input.files[0]
  }
}

// サーバーにCSVファイルをアップロードする
async function uploadFile() {
  if (!file.value) {
    uploadStatus.value = 'ファイルが選択されていません。'
    return
  }

  const formData = new FormData()
  formData.append('file', file.value)

  try {
    const response = await fetch(`${apiBaseUrl}/api/File/upload`, {
      method: 'POST',
      body: formData,
    })

    if (!response.ok) {
      throw new Error('アップロード失敗')
    }

    const result = await response.json()
    uploadedFileName.value = result.fileName
    uploadStatus.value = 'ファイルが正常にアップロードされました！'
  } catch (error: any) {
    uploadStatus.value = `Error: ${error.message}`
  }
}
</script>
