<script setup>
import JourneySection from './JourneySection.vue';

const works = [
  {
    id: '1',
    name: 'Soca AI',
    title: 'Soca AI',
    url: 'https://soca.ai',
    description:
      'In MSIB Batch 4, I took part in an internship program at Soca AI. Soca AI is a company that has a web application focused on content creation and powered by generative AI. At Soca AI, I contribute to building, creating, and managing its front-end applications.',
    logoSrc: '/images/works/soca-ai-logo.png',
    tag: 'Internship',
    stacks: [
      {
        name: 'Vue.js',
        iconClass: 'devicon-vuejs-plain colored',
      },
      {
        name: 'React',
        iconClass: 'devicon-react-original colored',
      },
      {
        name: 'Bootstrap',
        iconClass: 'devicon-bootstrap-plain colored',
      },
    ],
  },
  {
    id: '2',
    name: 'Forus',
    title: 'Forus',
    url: 'https://forus-beta.vercel.app',
    description:
      'Forus is a forum app I built to fulfill my submission project in a Dicoding course: Menjadi React Web Developer Expert. I built this front-end app by consuming the data in the provided REST API. The app uses React as the main library and its ecosystem.',
    logoSrc: '/images/works/forus-logo.png',
    tag: 'Featured',
    stacks: [
      {
        name: 'React',
        iconClass: 'devicon-react-original colored',
      },
      {
        name: 'Redux',
        iconClass: 'devicon-redux-original colored',
      },
      {
        name: 'Tailwind CSS',
        iconClass: 'devicon-tailwindcss-plain colored',
      },
      {
        name: 'Storybook',
        iconClass: 'devicon-storybook-plain colored',
      },
    ],
  },
  {
    id: '3',
    name: 'Koltra',
    title: 'Koltra',
    url: 'https://alfayeddennita.github.io/koltra',
    description:
      'Koltra is a news app I created to fulfill my submission project in a Dicoding course. The course is titled "Belajar Dasar Pemrograman Web". I used vanilla technologies to create the app without using any complex frameworks and libraries.',
    logoSrc: '/images/works/koltra-logo.png',
    tag: 'Latest',
    stacks: [
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
    id: '4',
    name: 'More, more, more!',
    title: 'My GitHub Account',
    url: 'https://github.com/AlfayedDennita',
    description:
      "That's it, of course, I can't show all of my work here. I still have other projects that you can see via my GitHub account. There are even several projects there that are not related to web development. Just feel free to explore it!",
    logoSrc: '/images/works/others.png',
    tag: 'Others',
    stacks: null,
  },
];
</script>

<template>
  <JourneySection
    id="works"
    title="Several of My Creations"
    icon-class="fas fa-shapes"
    icon-color-variant="primary"
    description="Below are several works that I created myself or with my awesome team."
  >
    <div class="works-section__works">
      <article v-for="work in works" :key="work.id" class="works-section__work">
        <div class="works-section__work-banner">
          <img class="works-section__work-banner-image" :src="work.logoSrc" :alt="work.name" />
        </div>
        <div class="works-section__work-content">
          <p class="works-section__work-tag">#{{ work.tag }}</p>
          <h3 class="works-section__work-name">
            <a
              v-if="work.url"
              class="works-section__work-link"
              :href="work.url"
              target="_blank"
              rel="external"
              :title="'Visit ' + work.title"
            >
              {{ work.name }}
              <i class="fas fa-arrow-up-right-from-square works-section__work-external-icon" />
            </a>
            <template v-else>
              {{ work.name }}
            </template>
          </h3>
          <p class="works-section__work-description">{{ work.description }}</p>
          <ul class="no-list works-section__work-stacks">
            <li v-for="stack in work.stacks" :key="stack.name" class="works-section__work-stack">
              <i
                class="works-section__work-stack-icon"
                :class="stack.iconClass"
                :title="stack.name"
              />
            </li>
          </ul>
        </div>
      </article>
    </div>

    <img
      class="works-section__decoration"
      src="images/decorations/yellow-subtle-waves.svg"
      alt=""
    />
  </JourneySection>
</template>

<style scoped>
.works-section__works {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.works-section__work {
  display: flex;
  flex-direction: column;
  background-color: var(--bg-color);
  border-radius: 0.5rem;
  overflow: hidden;
}

@media (width >= 768px) {
  .works-section__work {
    flex-direction: row;
  }
}

.works-section__work-banner {
  flex-shrink: 0;
  width: 100%;
  aspect-ratio: 16 / 9;
  display: flex;
  justify-content: center;
  align-items: center;
}

@media (width >= 768px) {
  .works-section__work-banner {
    max-width: 20rem;
  }
}

.works-section__work:nth-child(odd) .works-section__work-banner {
  background-color: rgba(var(--primary-color-rgb), 0.1);
}

.works-section__work:nth-child(even) .works-section__work-banner {
  background-color: rgba(var(--secondary-color-rgb), 0.1);
}

.works-section__work-banner-image {
  width: 30%;
}

.works-section__work-content {
  display: flex;
  flex-direction: column;
  padding: 1.5rem;
  background-color: var(--gray-0);
}

@media (width >= 768px) {
  .works-section__work-content {
    padding: 2rem;
  }

  .works-section__work:nth-child(even) .works-section__work-content {
    order: -1;
  }
}

.works-section__work-tag {
  font-size: 0.9rem;
  font-weight: 600;
}

.works-section__work-name {
  font-family: var(--heading-font-family);
  font-size: 1.75rem;
  font-weight: 700;
}

@media (width >= 768px) {
  .works-section__work-name {
    font-size: 2rem;
  }
}

.works-section__work-link {
  display: inline-flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.5rem;
}

.works-section__work-external-icon {
  font-size: 0.6rem;
  opacity: 0.25;
  transition: opacity 0.25s;
}

.works-section__work-link:is(:hover, :focus) .works-section__work-external-icon {
  opacity: 0.75;
}

.works-section__work-stacks {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  align-items: center;
  margin-top: 2.5rem;
}

.works-section__work-stack-icon {
  font-size: 1.5rem;
}

.works-section__decoration {
  z-index: -1;
  inset: 20% auto auto -10rem;
  position: absolute;
  width: 50rem;
  height: 45rem;
  opacity: 0.75;
}
</style>
