<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
  iconClass: {
    type: String,
    default: null,
  },
  description: {
    type: String,
    default: null,
  },
});
</script>

<template>
  <section class="journey-section">
    <div class="container journey-section__container">
      <header class="journey-section__header">
        <div class="journey-section__title">
          <i v-if="iconClass" class="journey-section__title-icon" :class="iconClass" />
          <h2 class="journey-section__title-text">{{ title }}</h2>
        </div>
        <p class="journey-section__description">{{ description }}</p>
      </header>
      <slot />
    </div>
  </section>
</template>

<style scoped>
.journey-section__container {
  --container-breakpoint: var(--bp-large);

  position: relative;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding: 5rem 1rem;
}

.journey-section__header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.journey-section__title {
  position: relative;
}

.journey-section__title-text {
  font-family: var(--heading-font-family);
  font-size: 3rem;
  font-weight: 700;
}

.journey-section__title-icon {
  z-index: -1;
  position: absolute;
  inset: -1rem auto auto -1rem;
  font-size: 3rem;
  color: var(--primary-color);
  opacity: 0.25;
}

.journey-section__description {
  font-size: 1.15rem;
  font-weight: 500;
}
</style>
