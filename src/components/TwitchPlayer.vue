<script setup lang="ts">
import {onMounted} from "vue";

const props = defineProps<{
  channel: string;
}>();

let player;
let intervalTest: number;

function loadTwitch() {
  player = new window.Twitch.Player(`twitchPlayer-${props.channel}`, {
    width: '100%',
    height: '100%',
    channel: props.channel,
    parent: 'localhost'
  });
}

onMounted(() => {
  intervalTest = setInterval(() => {
    if (window.Twitch && window.Twitch.Player) {
      loadTwitch();
      clearInterval(intervalTest);
    }
  }, 500);
})
</script>

<template>
  <div class="twitch-player" :id="`twitchPlayer-${channel}`"/>
</template>

<style scoped>
.twitch-player {
  width: 100%;
  height: 100%;
}
</style>
