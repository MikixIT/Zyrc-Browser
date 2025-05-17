<script setup lang="ts">
import Sidebar from "./components/Sidebar.vue";
import BrowserWindow from "./components/BrowserWindow.vue";
</script>

<template>
  <div id="app" class="browser-ui-font">
    <Sidebar />
    <BrowserWindow />
  </div>
</template>

<style scoped>
.flex {
  display: flex;
}
.h-screen {
  height: 100vh;
}

aside {
  width: 260px;
  background: #18181b;
  color: #fff;
  border-right: 1px solid #23232b;
  display: flex;
  flex-direction: column;
  min-width: 200px;
  max-width: 320px;
  box-shadow: 2px 0 8px #0002;
}

.browser-window {
  flex: 1;
  background: #f8fafc;
  display: flex;
  flex-direction: column;
  min-width: 0;
  overflow: hidden;
  position: relative;
}

.browser-navbar {
  height: 48px;
  background: #fff;
  border-bottom: 1px solid #e5e7eb;
  display: flex;
  align-items: center;
  padding: 0 16px;
  font-size: 1rem;
  font-weight: 500;
  box-shadow: 0 1px 4px #0001;
}

.browser-content {
  flex: 1;
  background: #fff;
  overflow: auto;
}

::-webkit-scrollbar {
  width: 8px;
  background: transparent;
}
::-webkit-scrollbar-thumb {
  background: #d1d5db;
  border-radius: 4px;
}

@media (max-width: 700px) {
  aside {
    width: 56px;
    min-width: 56px;
  }
}
</style>
