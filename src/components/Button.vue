<template>
  <button
    :class="['nsf9-button', isOver && 'active']"
    @mouseenter="handleMouse(true)"
    @mouseleave="handleMouse(false)"
  >
    <slot></slot>
  </button>
</template>

<script>
import { nextTick, ref, watchEffect } from "vue";

export default {
  name: "Button",
  props: {
    active: {
      type: Boolean,
    },
  },
  setup(props) {
    const isOver = ref(props.active);
    function handleMouse(flag) {
      isOver.value = flag;
    }
    return {
      isOver,
      handleMouse,
    };
  },
};
</script>

<style lang="scss" scoped>
.nsf9-button {
  margin: 4px;
  padding: 8px 12px;
  border: 2px solid transparent;
  outline: none;
  background-color: $button-bg;
  color: #fff;
  min-width: 100px;
  transition: all 4s linear;
  opacity: 1;

  & + .nsf9-button {
    margin-left: 24px;
  }

  &:focus {
    @extend .active;
  }
}

@keyframes bink {
  0% {
    // opacity: 0.2;
    color: #fff;
    border-image-source: radial-gradient(
      60% 60%,
      transparent 0px,
      transparent 100%,
      #fff 100%
    );
  }

  50% {
    // opacity: 0.4;
    color: $primary;
    border-image-source: radial-gradient(
      60% 60%,
      transparent 0px,
      transparent 100%,
      $primary 100%
    );
  }
}

.active {
  border-image-source: radial-gradient(
    60% 60%,
    transparent 0px,
    transparent 100%,
    $primary 100%
  );
  border-image-outset: 8px;
  border-image-slice: 1;
  border-width: 2px;
  border-style: solid;
  animation: bink 1s infinite linear;
}
</style>
