<script setup>
import Dialog from "./components/Dialog.vue";
import { nextTick, onMounted, ref } from "vue";
import Button from "@/components/Button.vue";

const dialogVisible = ref(false);
const active = ref(1);
const video = ref(null)
function handleClick(mode) {
  setTimeout(() => {
    alert(mode + " start failed.");
  }, 800);
  dialogVisible.value = false;
}
function handleClose() {
  return false;
}

function handleClickStart(e) {
  dialogVisible.value = true
  requestFullScreen()
}
function requestFullScreen() {
  if (document.fullscreenElement) {
    return
  }
  container.value.requestFullscreen()
}
const button = ref(null);
const container = ref(null);
onMounted(() => {
  nextTick(() => {
    button.value.$el.focus();
  });
});
document.addEventListener('click', () => {
  video.value.muted = false
  requestFullScreen()
})
</script>

<template>
  <div class="demo" ref="container">
    <video
      autoplay
      muted
      playsinline
      src="./assets/video/nfs9.mp4"
      ref="video"
      loop
    ></video>
    <div class="start">
      <Button ref="button" active @click="handleClickStart">Start</Button>
    </div>

    <Dialog
      v-model:visible="dialogVisible"
      :before-close="handleClose"
      title="selection"
      width="30%"
    >
      <span>Select your transmission.</span>
      <template v-slot:footer>
        <div class="dialog-footer">
          <Button @click="handleClick('Manual')">Manual</Button>
          <Button @click="handleClick('Auto')">Auto</Button>
        </div>
      </template>
    </Dialog>
  </div>
</template>

<style scoped lang="scss">
.demo {
  //width: 100vw;
  //height: 100vh;
  //overflow: hidden;
  video {
    position: fixed;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .start {
    position: absolute;
    left: 90%;
    top: 90%;
    transform: translate(-50%, -50%);
  }
}
</style>
