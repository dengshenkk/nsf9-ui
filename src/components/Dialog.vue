<template>
  <div class="nsf9-dialog__wrapper" v-if="visible">
    <div class="nfs9-dialog" :style="{ width }">
      <div class="nfs9-dialog__header">
        <span class="nfs9-dialog__title">{{ title }}</span>
        <span
          class="nfs9-dialog__headerbtn"
          v-if="closeable"
          @click="emits('update:visible', false)"
        >
          <slot name="icon-close">
            <span>X</span>
          </slot>
        </span>
      </div>
      <div class="nfs9-dialog__body">
        <slot></slot>
      </div>

      <div class="nfs9-dialog__footerWrapper">
        <div class="nfs9-dialog__footer">
          <slot name="footer">222</slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dialog",
};
</script>

<script setup>
defineProps({
  visible: Boolean,
  title: String,
  closeable: {
    type: Boolean,
    default: false,
  },
  width: String,
});

const emits = defineEmits(["update:visible"]);
</script>

<style lang="scss" scoped>
.nsf9-dialog__wrapper {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
  color: #ffffff;
}

.nfs9-dialog {
  font-weight: bold;
  position: relative;
  margin: 15vh auto 50px;
  background: #fff;
  border-radius: 2px;
  box-shadow: 0 1px 3px rgb(0 0 0 / 30%);
  border: $border-width solid $border-color;
  // linear-gradient(45deg, #cc95c0 50%, #dbd4b4 0);
  background: linear-gradient(
    135deg,
    #444 25%,
    #000 0,
    #000 50%,
    #444 0,
    #444 75%,
    #000 0
  );
  background-size: 16px 16px;

  &__header {
    padding: 16px;
    display: flex;
    border-bottom: $border-width solid $border-color;
  }
  &__title {
    flex: 1;
  }
  &__headerbtn {
    width: 16px;
    cursor: pointer;
  }

  &__body {
    padding: 30px 20px;
    font-size: 14px;
    word-break: break-all;
    background: rgba($primary-bg, 0.5);
  }

  &__footerWrapper {
    padding: 10px 0;
    text-align: right;
    border-top: $border-width solid $border-color;
  }
  &__footer {
    padding: 0 16px;
    background-color: rgba($primary-bg, 0.5);
  }
}
</style>
