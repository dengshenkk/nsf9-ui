<script setup>
import Dialog from "./components/Dialog.vue";
import { nextTick, onMounted, ref } from "vue";
import Button from "@/components/Button.vue";

const dialogVisible = ref(false);
const active = ref(1);
function handleClick(mode) {
  setTimeout(() => {
    alert(mode + " start failed.");
  }, 800);
  dialogVisible.value = false;
}
function handleClose() {
  return false;
}

const button = ref(null);
onMounted(() => {
  nextTick(() => {
    button.value.$el.focus();
  });
});
</script>

<template>
  <div class="demo">
    <video
      autoplay
      muted
      playsinline
      src="./assets/video/nfs9.mp4"
      loop
    ></video>
    <div class="start">
      <Button ref="button" active @click="dialogVisible = true">Start</Button>
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
