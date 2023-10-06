<script setup>
import { ref, onMounted } from 'vue';

const dayGreeting = ref({
  icon: null,
  text: null,
});

onMounted(() => {
  const hours = new Date().getHours();
  let greetingIcon;
  let greetingText;

  if (hours >= 22) {
    greetingIcon = 'fas fa-moon';
    greetingText = 'Good Night!';
  } else if (hours >= 18) {
    greetingIcon = 'fas fa-cloud-moon';
    greetingText = 'Good Evening!';
  } else if (hours >= 12) {
    greetingIcon = 'fas fa-sun';
    greetingText = 'Good Afternoon!';
  } else {
    greetingIcon = 'fas fa-mug-saucer';
    greetingText = 'Good Morning!';
  }

  dayGreeting.value = {
    icon: greetingIcon,
    text: greetingText,
  };
});
</script>

<template>
  <section class="jumbotron">
    <div class="container jumbotron__container">
      <div class="jumbotron__main-content">
        <div class="jumbotron__photo-container">
          <img
            class="jumbotron__photo"
            src="/images/personal-photo.png"
            alt="Muhammad Alfayed Dennita"
          />
        </div>

        <div class="jumbotron__text-content">
          <p class="jumbotron__greeting">
            <span>Hi, there!</span>
            <span v-if="dayGreeting?.icon && dayGreeting?.text" class="jumbotron__greeting-day">
              <i class="jumbotron__greeting-day-icon" :class="dayGreeting.icon" />
              {{ dayGreeting.text }}
            </span>
          </p>
          <p class="jumbotron__pre-heading">I am</p>
          <h2 class="jumbotron__heading">Muhammad Alfayed Dennita</h2>
          <p class="jumbotron__welcome">Welcome to my journey page, let's deep dive together!</p>
        </div>
      </div>

      <a class="jumbotron__cta" href="#about" title="Explore">
        <span>Let's Go!</span>
        <div class="jumbotron__cta-icons">
          <i class="fas fa-chevron-down jumbotron__cta-icon" />
          <i class="fas fa-chevron-down jumbotron__cta-icon" />
        </div>
      </a>
    </div>

    <div class="jumbotron__decoration" />
  </section>
</template>

<style scoped>
.jumbotron {
  padding-block: 3.5rem 1.5rem;
}

@media (width >= 768px) {
  .jumbotron {
    padding-block: 4rem 2rem;
  }
}

.jumbotron__container {
  --container-breakpoint: var(--bp-large);

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 3rem;
  padding: 1rem 2rem;
  text-align: center;
}

@media (width >= 768px) {
  .jumbotron__container {
    padding: 5rem 4rem 4rem 4rem;
    gap: 6rem;
  }
}

.jumbotron__main-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

@media (width >= 768px) {
  .jumbotron__main-content {
    flex-direction: row;
    justify-content: space-between;
    text-align: initial;
    gap: 3rem;
  }
}

.jumbotron__photo-container {
  order: 2;
  flex-shrink: 0;
  width: 10rem;
  aspect-ratio: 1 / 1;
  padding: 0.25rem;
  margin-block: 1rem;
  border-radius: 50%;
  background-image: linear-gradient(135deg, var(--primary-color) 50%, var(--secondary-color) 50%);
}

@media (width >= 768px) {
  .jumbotron__photo-container {
    order: initial;
  }
}

.jumbotron__photo {
  width: 100%;
  aspect-ratio: 1 / 1;
  border-radius: 50%;
  border: 0.25rem solid var(--bg-color);
}

.jumbotron__text-content {
  display: contents;
}

@media (width >= 768px) {
  .jumbotron__text-content {
    order: initial;
    display: flex;
    flex-direction: column;
  }
}

.jumbotron__greeting {
  order: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.5rem;
  font-size: 1.15rem;
}

@media (width >= 768px) {
  .jumbotron__greeting {
    justify-content: flex-start;
    margin-bottom: 1rem;
    font-size: 1.25rem;
  }
}

.jumbotron__greeting-day {
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  font-weight: 600;
}

.jumbotron__greeting-day-icon {
  font-size: 1rem;
}

@media (width >= 768px) {
  .jumbotron__greeting-day-icon {
    font-size: 1.1rem;
  }
}

.jumbotron__pre-heading {
  order: 3;
  font-size: 1.15rem;
  font-weight: 500;
}

@media (width >= 768px) {
  .jumbotron__pre-heading {
    font-size: 1.25rem;
  }
}

.jumbotron__heading {
  order: 4;
  position: relative;
  margin-block: 0.5rem;
  font-family: var(--heading-font-family);
  font-size: 2.25rem;
  font-weight: 700;
  line-height: 1;
}

@media (width >= 768px) {
  .jumbotron__heading {
    font-size: 3rem;
    line-height: 1.25;
  }
}

.jumbotron__heading::before {
  content: '';
  z-index: -1;
  position: absolute;
  inset: 40% -0.5rem 0 -0.5rem;
  background-image: linear-gradient(
    to right,
    rgba(var(--primary-color-rgb), 0.25) 50%,
    rgba(var(--secondary-color-rgb), 0.25) 50%
  );
  clip-path: polygon(15% 0, 100% 0, 85% 100%, 0 100%);
}

.jumbotron__welcome {
  order: 5;
  margin-top: 0.5rem;
}

@media (width >= 768px) {
  .jumbotron__welcome {
    font-size: 1.1rem;
  }
}

.jumbotron__cta {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  font-size: 0.85rem;
}

@media (width >= 768px) {
  .jumbotron__cta {
    font-size: 0.95rem;
  }
}

.jumbotron__cta-icons {
  display: flex;
  flex-direction: column;
}

.jumbotron__cta-icon {
  font-size: 1rem;
  line-height: 0.5;
  animation: cta-icon 1.5s infinite;
  transition: color 0.25s;
}

.jumbotron__cta:hover .jumbotron__cta-icon:first-child {
  color: var(--primary-color);
}

.jumbotron__cta:hover .jumbotron__cta-icon:last-child {
  color: var(--secondary-color);
}

.jumbotron__cta-icon:last-child {
  animation-delay: 0.1s;
}

@keyframes cta-icon {
  0% {
    translate: 0 0rem;
  }
  50% {
    translate: 0 0.25rem;
  }
  100% {
    translate: 0 0rem;
  }
}

.jumbotron__decoration {
  z-index: -1;
  inset: -15rem -15rem auto auto;
  position: fixed;
  height: 30rem;
  aspect-ratio: 1 / 1;
  border-radius: 50%;
  background-image: radial-gradient(
    rgba(var(--primary-color-rgb), 0.1) 20%,
    rgba(var(--secondary-color-rgb), 0.1),
    transparent 70%
  );
}

@media (width >= 768px) {
  .jumbotron__decoration {
    inset: -30rem -30rem auto auto;
    height: 60rem;
  }
}
</style>
