<script setup>
defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
});
defineEmits(['update:modelValue']);
</script>

<template>
  <button
    class="hamburger-button"
    :class="{ 'hamburger-button--open': modelValue }"
    :title="(modelValue ? 'Close' : 'Open') + ' Navigation Menu'"
    @click="$emit('update:modelValue', !modelValue)"
  >
    <div v-for="i in 3" :key="i" class="hamburger-button__line" />
  </button>
</template>

<style scoped>
.hamburger-button {
  width: 1.8rem;
  height: 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-end;
}

.hamburger-button__line {
  width: 100%;
  height: 0.25rem;
  background-color: var(--text-color);
  border-radius: 0.25rem;
  transform-origin: right;
  transition:
    rotate 0.25s,
    width 0.1s;
}

.hamburger-button--open .hamburger-button__line:first-child {
  rotate: -45deg;
}

.hamburger-button--open .hamburger-button__line:nth-child(2) {
  width: 0;
}

.hamburger-button--open .hamburger-button__line:last-child {
  rotate: 45deg;
}
</style>
