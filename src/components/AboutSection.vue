<script setup>
import JourneySection from './JourneySection.vue';
</script>

<template>
  <JourneySection
    id="about"
    title="Who Am I?"
    icon-class="fas fa-user-ninja"
    icon-color-variant="primary"
    description="First, let's start by knowing about me."
  >
    <div class="about-section__content">
      <p>
        Hi 👋. My name is <strong>Muhammad Alfayed Dennita</strong>, student at Sriwijaya State
        Polytechnic, Palembang 🏫. I am majoring in Informatics Management and am currently in my
        7th semester. In line with my major, I also became a junior
        <strong>web developer</strong> 👨‍💻 focusing on front-end development. I like designing UI/UX
        with code 🎨, which is why I focus on front-end development rather than back-end
        development. Despite everything, I'm still learning back-end development to improve my web
        development skills.
      </p>
      <p>
        Currently, I am a student in <strong>Bangkit 2023 Batch 2</strong> 💻. I have joined the
        <strong>Cloud Computing</strong> ☁️ learning path. The main reason I joined that learning
        path is because I want to complete my other puzzle piece in the web development area. I need
        to know how to create a robust backend application and deploy it to the internet,
        specifically using the <strong>Google Cloud</strong> platform. After graduation, I hope to
        be able to apply what I get in the program so I can become a web developer completely 💫.
      </p>
      <p>
        So this is an overview of me. If you want to know more about me, you can scroll through this
        journey page. I hope we can work together to create something amazing in the future 🚀.
      </p>
    </div>

    <img
      class="about-section__decoration"
      src="https://storage.googleapis.com/fayden-journey/images/decorations/yellow-chevrons.svg"
      alt=""
    />
  </JourneySection>
</template>

<style scoped>
.about-section__content {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 45rem;
  margin-inline: auto;
}

.about-section__decoration {
  z-index: -1;
  position: absolute;
  inset: auto auto 20% -12.5rem;
  width: 31rem;
  height: 18.8rem;
  scale: 0.5;
  opacity: 0.075;
}

@media (width >= 768px) {
  .about-section__decoration {
    inset: auto auto 20% -20.5rem;
    opacity: 0.1;
  }
}
</style>
