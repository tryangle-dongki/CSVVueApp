<template>
  <div id="app">
    <Upload />
  </div>
</template>

<script setup lang="ts">
// Uploadコンポーネントをインポート
import Upload from './components/Upload.vue'
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
