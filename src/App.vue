<script setup lang="ts">

import TwitchPlayer from "@/components/TwitchPlayer.vue";
import {onMounted, ref, watch} from "vue";

const playerIsResizing = ref(false);
const playerHeight = ref(570);

function resizePlayer(evt: PointerEvent) {
  if (!playerIsResizing.value) return
  console.log("doing?")
  const pos = Math.abs(evt.clientY)
  if (pos < 285) {
    playerHeight.value = 285;
  } else if (pos >= 560 && pos <= 580) {
    playerHeight.value = 570;
  } else if (pos > 700) {
    playerHeight.value = 700;
  } else {
    playerHeight.value = pos;
  }
}

watch(playerHeight, () => {
  if (playerHeight.value < 185 || playerHeight.value > 800) return
  document.documentElement.style.setProperty('--player-height', `${playerHeight.value}px`)
})

onMounted(() => {
  window.addEventListener('pointermove', resizePlayer);
  window.addEventListener('pointerup', () => {
    playerIsResizing.value = false;
  })
})
</script>

<template>
  <main class="app-container">
    <div class="video-container">
      <TwitchPlayer :class="playerIsResizing ? 'inactive' : ''" channel="ironmouse"/>
      <div class="resize-container" @pointerdown="playerIsResizing = true" @pointerup="playerIsResizing = false">
        <div class="resize-handle"/>
      </div>
      <TwitchPlayer :class="playerIsResizing ? 'inactive' : ''" channel="AlveusSanctuary"/>
    </div>
    <div class="sidebar">
      <div class="controls">
        <h4>Multi-Twitch</h4>
      </div>
      <iframe src="https://www.twitch.tv/embed/ironmouse/chat?parent=localhost&darkpopout" width="100%" height="100%"></iframe>
    </div>
  </main>
</template>

<style scoped>
.app-container {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 340px;
  grid-template-rows: 1fr;
}

.sidebar {
  background-color: var(--sub-bg);
  border-left: 1px solid var(--bd);
  display: grid;
  grid-template-rows: 40px 1fr;
}

.sidebar .controls {
  background: var(--sub-bg);
  border-bottom: solid 1px var(--bd);
  padding: 12px;
  display: flex;
  align-items: center;
}

.sidebar .controls h4 {
  margin: 0;
  font-size: 14px;
  font-weight: 600;
}

.sidebar iframe {
  border: none;
}

.video-container {
  width: 100%;
  height: 100vh;
  display: grid;
  grid-template-rows: var(--player-height) 0 1fr;
}

.video-container .resize-container {
  width: 100%;
  height: 10px;
  position: relative;
  display: flex;
  align-items: center;
  cursor: n-resize;
  transform: translateY(-5px);
  z-index: 999;
}

.video-container .resize-container .resize-handle {
  width: 100%;
  height: 1px;
  background: var(--bd);
}

.resize-container:hover .resize-handle {
  background-color: var(--accent);
}

.inactive {
  pointer-events: none;
}
</style>
