<script setup lang="ts">

import TwitchPlayer from "@/components/TwitchPlayer.vue";
</script>

<template>
  <main class="app-container">
    <div class="video-container">
      <TwitchPlayer channel="ironmouse"/>
      <TwitchPlayer channel="AlveusSanctuary"/>
    </div>
    <div class="sidebar">
      <div class="controls">
        <p>MultiTwitch</p>
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
  grid-template-rows: 50px 1fr;
}

.sidebar .controls {
  background: var(--sub-bg);
  border-bottom: solid 1px var(--bd);
}

.sidebar iframe {
  border: none;
}

.video-container {
  width: 100%;
  height: 100vh;
  display: grid;
  grid-template-rows: 1.5fr 1fr;
}
</style>
