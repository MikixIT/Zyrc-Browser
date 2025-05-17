<template>
  <div class="browser-window">
    <div class="browser-content">
      <webview
        :src="url"
        class="browser-webview"
        allowpopups
        webpreferences="nativeWindowOpen=yes"
      ></webview>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const url = ref("https://www.google.com");
</script>

<style scoped>
.browser-window {
  flex: 1;
  display: flex;
  flex-direction: column;
  min-width: 0;
  min-height: 0;
  height: 100%;
  background: #f8fafc;
}
.browser-content {
  flex: 1;
  min-height: 0;
  height: 100%;
  overflow: hidden;
  display: flex;
}
.browser-webview {
  width: 100%;
  height: 100%;
  border: none;
  background: #fff;
  flex: 1;
  min-width: 0;
  min-height: 0;
}
</style>
