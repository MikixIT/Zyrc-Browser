<template>
  <div class="sidebar-hotspot" @mouseenter="openSidebar"></div>
  <transition name="sidebar-fade">
    <aside
      v-if="isOpen"
      class="sidebar"
      @mouseleave="autoClose"
      @mouseenter="cancelAutoClose"
    >
      <div class="sidebar-header">
        <img
          src="/Zyrc.ico"
          alt="Logo Zyrc"
          class="zyrc-icon"
          @click="onLogoClick"
        />
        <h2 class="zyrc-logo glass-logo" @click="onLogoClick">Zyrc</h2>
        <button @click="addTab" class="add-tab" title="Nuova Tab">＋</button>
      </div>
      <transition-group name="tab-list" tag="ul" class="sidebar-tabs">
        <li
          v-for="tab in tabs"
          :key="tab.id"
          :class="[
            'sidebar-tab',
            {
              active: tab.id === activeTabId,
              'has-close': hoveredTab === tab.id,
            },
          ]"
          @click="setActiveTab(tab.id)"
          @mouseenter="hoveredTab = tab.id"
          @mouseleave="hoveredTab = null"
        >
          <span>{{ tab.title }}</span>
          <transition name="close-x">
            <button
              v-if="hoveredTab === tab.id"
              class="close-tab-btn"
              @click.stop="closeTab(tab.id)"
              title="Chiudi"
            >
              <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
                <path
                  d="M5 5L13 13M13 5L5 13"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                />
              </svg>
            </button>
          </transition>
        </li>
      </transition-group>
    </aside>
  </transition>
</template>

<script setup lang="ts">
import { ref } from "vue";

const isOpen = ref(false);
let closeTimeout: number | null = null;

function openSidebar() {
  isOpen.value = true;
  cancelAutoClose();
}

function autoClose() {
  closeTimeout = window.setTimeout(() => {
    isOpen.value = false;
  }, 600);
}
function cancelAutoClose() {
  if (closeTimeout) {
    clearTimeout(closeTimeout);
    closeTimeout = null;
  }
}

const tabs = ref([
  { id: 1, title: "Nuova Tab", url: "https://example.com" },
  { id: 2, title: "Zyrc Docs", url: "https://tauri.app" },
]);

const activeTabId = ref(1);
const hoveredTab = ref<number | null>(null);

function setActiveTab(id: number) {
  activeTabId.value = id;
}

function addTab() {
  const newId = Date.now();
  tabs.value.push({ id: newId, title: "New Tab", url: "https://google.com" });
  activeTabId.value = newId;
}

function closeTab(id: number) {
  const idx = tabs.value.findIndex((tab) => tab.id === id);
  if (idx !== -1) {
    tabs.value.splice(idx, 1);

    if (activeTabId.value === id) {
      if (tabs.value.length) {
        activeTabId.value = tabs.value[Math.max(0, idx - 1)].id;
      } else {
        activeTabId.value = 0;
      }
    }
  }
}

function onLogoClick() {
  window.open("https://zyrc.dev", "_blank");
}
</script>

<style scoped>
.zyrc-logo {
  font-family: "Playwrite DK Loopet", cursive;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  letter-spacing: 2px;
  font-size: 2rem;
  color: #fff;
  text-shadow: 0 2px 16px rgba(0, 0, 0, 0.18);
}

.zyrc-icon {
  width: 72px; /* più grande */
  height: 72px;
  margin-bottom: 8px;
  margin-top: 4px;
  border-radius: 16px;
  box-shadow: 0 4px 24px 0 rgba(0, 0, 0, 0.13);
  object-fit: contain;
  background: rgba(255, 255, 255, 0.1);
  transition: transform 0.38s cubic-bezier(0.77, 0, 0.18, 1),
    box-shadow 0.38s cubic-bezier(0.77, 0, 0.18, 1), background 0.28s;
}
.zyrc-icon:hover {
  transform: scale(1.13);
  box-shadow: 0 8px 36px 0 rgba(255, 255, 255, 0.18),
    0 4px 24px 0 rgba(0, 0, 0, 0.18);
  background: rgba(255, 255, 255, 0.22);
  cursor: pointer;
}

.sidebar-hotspot {
  position: fixed;
  top: 0;
  left: 0;
  width: 18px;
  height: 100vh;
  z-index: 100;
  background: transparent;
  cursor: pointer;
}

.sidebar {
  width: 100px;
  min-width: 200px;
  max-width: 320px;
  height: 100vh;
  background: rgba(36, 37, 46, 0.55);
  color: #fff;
  border-right: 1.5px solid rgba(255, 255, 255, 0.13);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  box-shadow: 8px 0 32px 0 rgba(0, 0, 0, 0.12);
  backdrop-filter: blur(18px) saturate(160%);
  -webkit-backdrop-filter: blur(18px) saturate(160%);
  padding: 28px 0;
  border-radius: 0 24px 24px 0;
  border-left: 0.5px solid rgba(255, 255, 255, 0.04);
  border-top: 0.5px solid rgba(255, 255, 255, 0.04);
  border-bottom: 0.5px solid rgba(255, 255, 255, 0.04);
  box-sizing: border-box;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 101;
}

.sidebar-header {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  margin-bottom: 18px;
  flex-shrink: 0;
}

.add-tab {
  margin-top: 6px;
  font-size: 1.5rem;
  background: rgba(255, 255, 255, 0.08);
  border: none;
  color: #fff;
  cursor: pointer;
  border-radius: 8px;
  padding: 4px 12px;
  transition: background 0.2s, color 0.2s, box-shadow 0.2s;
  box-shadow: 0 2px 8px 0 rgba(0, 0, 0, 0.08);
}
.add-tab:hover {
  background: rgba(255, 255, 255, 0.18);
  color: #ffd700;
}
.sidebar-tab {
  width: 85%;
  min-height: 38px;
  max-height: 38px;
  padding: 0 12px 0 18px;
  margin: 0 0 12px 0;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  border-radius: 10px;
  cursor: pointer;
  background: rgba(255, 255, 255, 0.06);
  transition: background 0.2s, color 0.2s, box-shadow 0.2s, border 0.2s,
    padding-right 0.22s cubic-bezier(0.77, 0, 0.18, 1);
  color: #fff;
  font-size: 1rem;
  font-weight: 500;
  box-shadow: 0 1px 8px 0 rgba(0, 0, 0, 0.04);
  border: 1.5px solid transparent;
  backdrop-filter: blur(2px);
  overflow: hidden;
  user-select: none;
  position: relative;
  padding-right: 8px;
  box-sizing: border-box;
}
.sidebar-tab.has-close {
  padding-right: 32px;
}

.sidebar-tab span {
  flex: 1 1 auto;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  font-size: 1rem;
  font-weight: 500;
  padding-right: 0;
}

.sidebar-fade-enter-active,
.sidebar-fade-leave-active {
  transition: opacity 0.35s cubic-bezier(0.77, 0, 0.18, 1),
    transform 0.45s cubic-bezier(0.77, 0, 0.18, 1);
}
.sidebar-fade-enter-from,
.sidebar-fade-leave-to {
  opacity: 0;
  transform: translateX(-60px) scale(0.98);
  filter: blur(8px);
  pointer-events: none;
}
.sidebar-fade-enter-to,
.sidebar-fade-leave-from {
  opacity: 1;
  transform: translateX(0) scale(1);
  filter: blur(0);
}

.close-tab-btn {
  position: absolute;
  right: 6px;
  top: 50%;
  transform: translateY(-50%);
  margin-left: 0;
  background: rgba(255, 255, 255, 0.13);
  border: none;
  color: #fff;
  cursor: pointer;
  border-radius: 50%;
  font-size: 1.2rem;
  line-height: 1;
  padding: 2px 2px 0 2px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background 0.18s, color 0.18s, box-shadow 0.18s, scale 0.18s;
  box-shadow: 0 1px 4px 0 rgba(0, 0, 0, 0.1);
  opacity: 0.92;
}
.close-tab-btn:hover {
  background: #ff6b6b;
  color: #fff;
  scale: 1.18;
  box-shadow: 0 2px 8px 0 #ff6b6b44;
}
.close-tab-btn svg {
  display: block;
}

.close-x-enter-active,
.close-x-leave-active {
  transition: opacity 0.12s cubic-bezier(0.77, 0, 0.18, 1),
    transform 0.12s cubic-bezier(0.77, 0, 0.18, 1);
}
.close-x-enter-from,
.close-x-leave-to {
  opacity: 0;
  transform: scale(0.7) translateX(12px);
  filter: blur(2px);
}
.close-x-enter-to,
.close-x-leave-from {
  opacity: 1;
  transform: scale(1) translateX(0);
  filter: blur(0);
}

.tab-list-move {
  transition: transform 0.25s cubic-bezier(0.77, 0, 0.18, 1);
}
.tab-list-enter-active,
.tab-list-leave-active {
  transition: opacity 0.22s cubic-bezier(0.77, 0, 0.18, 1),
    transform 0.22s cubic-bezier(0.77, 0, 0.18, 1);
}
.tab-list-enter-from,
.tab-list-leave-to {
  opacity: 0;
  transform: scale(0.85) translateX(30px);
  filter: blur(2px);
}
.tab-list-enter-to,
.tab-list-leave-from {
  opacity: 1;
  transform: scale(1) translateX(0);
  filter: blur(0);
}
</style>
