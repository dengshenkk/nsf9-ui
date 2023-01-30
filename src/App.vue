<script setup>
import Dialog from "./components/Dialog.vue";
import { ref } from "vue";
import Button from "@/components/Button.vue";

const dialogVisible = ref(false);
const active = ref(1);
function handleClick(mode) {
  alert(mode + " start failed.");
  dialogVisible.value = false;
}
function handleClose() {
  return false;
}
</script>

<template>
  <div class="demo">
    <Button @click="dialogVisible = true" active>Start</Button>
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
  width: 1080px;
  margin: 20vh auto;
  display: flex;
  align-content: center;
  justify-content: center;
}
</style>
