<script setup>
import JourneySection from './JourneySection.vue';

const stacks = [
  {
    id: '1',
    title: 'Programming Languages',
    description: 'Several languages that I usually use, including markup languages.',
    iconClass: 'fas fa-language',
    items: [
      {
        name: 'HTML5',
        iconClass: 'devicon-html5-plain colored',
      },
      {
        name: 'CSS3',
        iconClass: 'devicon-css3-plain colored',
      },
      {
        name: 'JavaScript',
        iconClass: 'devicon-javascript-plain colored',
      },
    ],
  },
  {
    id: '2',
    title: 'Frameworks/Libraries/Tools',
    description: 'Frameworks, libraries, and tools that I use daily.',
    iconClass: 'fas fa-screwdriver-wrench',
    items: [
      {
        name: 'Node.js',
        iconClass: 'devicon-nodejs-plain colored',
      },
      {
        name: 'Vue.js',
        iconClass: 'devicon-vuejs-plain colored',
      },
      {
        name: 'React',
        iconClass: 'devicon-react-original colored',
      },
      {
        name: 'Express',
        iconClass: 'devicon-express-original colored',
      },
      {
        name: 'MySQL',
        iconClass: 'devicon-mysql-plain colored',
      },
      {
        name: 'Git',
        iconClass: 'devicon-git-plain colored',
      },
      {
        name: 'Figma',
        iconClass: 'devicon-figma-plain colored',
      },
    ],
  },
];
</script>

<template>
  <JourneySection
    id="stacks"
    title="Tech Stacks"
    icon-class="fas fa-cubes"
    icon-color-variant="secondary"
    description="These are technologies that I have learned and used to build amazing apps."
  >
    <div class="stacks-section__content">
      <article v-for="stack in stacks" :key="stack.id" class="stacks-section__article">
        <header class="stacks-section__article-header">
          <i class="stacks-section__article-icon" :class="stack.iconClass" />
          <h3 class="stacks-section__article-title">{{ stack.title }}</h3>
          <p class="stacks-section__article-description">
            {{ stack.description }}
          </p>
        </header>
        <ul class="no-list stacks-section__article-items">
          <li v-for="item in stack.items" :key="item.name" class="stacks-section__article-item">
            <i class="stacks-section__article-item-icon" :class="item.iconClass" />
            <p class="stacks-section__article-item-name">{{ item.name }}</p>
          </li>
        </ul>
      </article>
    </div>

    <img class="stacks-section__decoration" src="images/decorations/blue-dots.svg" alt="" />
  </JourneySection>
</template>

<style scoped>
.stacks-section__content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

@media (width >= 768px) {
  .stacks-section__content {
    grid-template-columns: repeat(2, 1fr);
  }
}

.stacks-section__article {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  border-radius: 0.5rem;
  padding: 2rem;
  background-color: var(--gray-0);
}

.stacks-section__article-header {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.stacks-section__article-icon {
  font-size: 1.5rem;
}

.stacks-section__article:first-child .stacks-section__article-icon {
  color: var(--primary-color);
}

.stacks-section__article:last-child .stacks-section__article-icon {
  color: var(--secondary-color);
}

.stacks-section__article-title {
  font-family: var(--heading-font-family);
  font-size: 1.25rem;
  font-weight: 500;
}

.stacks-section__article-description {
  font-size: 0.8rem;
}

.stacks-section__article-items {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: auto;
}

.stacks-section__article-item {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  padding: 0.2rem 0.5rem;
  border-radius: 0.25rem;
  background-color: var(--gray-1);
}

.stacks-section__article-item-name {
  font-size: 0.8rem;
}

.stacks-section__decoration {
  z-index: -1;
  position: absolute;
  inset: 10% -9.5rem auto auto;
  width: 20rem;
  height: 20rem;
  scale: 0.5;
  opacity: 0.1;
}
</style>
