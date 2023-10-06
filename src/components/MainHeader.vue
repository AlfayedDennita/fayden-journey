<script setup>
import { ref, watch, onMounted } from 'vue';
import { FocusTrap } from 'focus-trap-vue';

import HamburgerButton from './HamburgerButton.vue';

const windowScrollY = ref(window.scrollY);
const isOnSmallScreen = ref(window.matchMedia('(width < 768px)').matches);
const isNavShown = ref(false);
const isHeaderHidden = ref(false);

const navLinks = [
  {
    id: 'about',
    name: 'About',
  },
  {
    id: 'stacks',
    name: 'Stacks',
  },
  {
    id: 'works',
    name: 'Works',
  },
  {
    id: 'contacts',
    name: 'Contacts',
  },
];

watch(windowScrollY, (newWindowScrollY, prevWindowScrollY) => {
  if (newWindowScrollY > 100 && newWindowScrollY > prevWindowScrollY) {
    isHeaderHidden.value = true;
  } else {
    isHeaderHidden.value = false;
  }
});

watch(isNavShown, (newIsNavShown) => {
  if (newIsNavShown) {
    document.body.style.overflowY = 'hidden';
  } else {
    document.body.style.overflowY = 'auto';
  }
});

onMounted(() => {
  window.addEventListener('scroll', () => {
    windowScrollY.value = window.scrollY;
  });
  window.addEventListener('resize', () => {
    isOnSmallScreen.value = window.matchMedia('(width < 768px)').matches;
  });
});
</script>

<template>
  <FocusTrap :active="isNavShown && isOnSmallScreen">
    <header class="header" :class="{ 'header--hidden': isHeaderHidden }">
      <div class="container header__container">
        <h1 class="header__heading">
          <a class="header__heading-link" href="/" title="Fayden Journey">
            <img class="header__logo" src="/images/logo.png" alt="Fayden Logo" />
            <span class="sr-only">Fayden Journey</span>
          </a>
        </h1>

        <div class="header__hamburger-button-wrapper">
          <HamburgerButton v-model="isNavShown" />
        </div>

        <nav class="header__nav" :class="{ 'header__nav--shown': isNavShown }">
          <ul class="no-list header__nav-list">
            <li v-for="(link, index) in navLinks" :key="link.id" class="header__nav-item">
              <a
                class="header__nav-link"
                :class="{
                  'header__nav-link--separated': index + 1 === Math.floor(navLinks.length / 2),
                }"
                :href="'#' + link.id"
                :title="link.name"
                :tabindex="!isNavShown && isOnSmallScreen ? -1 : 0"
                @click="isNavShown = false"
              >
                {{ link.name }}
              </a>
            </li>
          </ul>
        </nav>
      </div>
    </header>
  </FocusTrap>
</template>

<style scoped>
.header {
  --header-height: 3.5rem;

  isolation: isolate;
  position: fixed;
  inset: 0 0 auto 0;
  height: var(--header-height);
  display: flex;
  align-items: center;
  background-color: var(--bg-color);
  transition: top 0.25s;
}

@media (width >= 768px) {
  .header {
    --header-height: 4rem;
  }
}

.header::after {
  content: '';
  position: absolute;
  inset: auto 0 0 0;
  display: block;
  height: 1px;
  background-color: var(--gray-1);
}

.header--hidden {
  top: calc(0px - var(--header-height));
}

.header__container {
  display: grid;
  grid-template-columns: repeat(2, auto);
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

@media (width >= 768px) {
  .header__container {
    grid-template-columns: auto;
    justify-content: center;
  }
}

.header__heading {
  display: flex;
  justify-content: center;
}

@media (width >= 768px) {
  .header__heading {
    grid-area: 1 / 1;
  }
}

.header__heading-link {
  z-index: 2;
  position: relative;
}

@media (width >= 768px) {
  .header__heading-link {
    padding: 0.5rem;
  }
}

.header__logo {
  width: 2rem;
  height: 2rem;
  object-fit: contain;
}

.header__hamburger-button-wrapper {
  display: contents;
}

.header__hamburger-button-wrapper > * {
  z-index: 2;
}

@media (width >= 768px) {
  .header__hamburger-button-wrapper {
    display: none;
  }
}

@media (width < 768px) {
  .header__nav {
    position: fixed;
    inset: var(--header-height) 0 0 0;
    translate: 100% 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
    background-color: var(--bg-color);
    overflow-y: auto;
    transition: translate 0.5s;
  }

  .header__nav--shown {
    translate: 0;
  }

  .header__nav-list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1.5rem;
    margin-block: auto;
  }

  .header__nav-item {
    transition: scale 0.5s;
  }

  .header__nav-item:has(.header__nav-link:is(:hover, :focus)) {
    scale: 1.25;
  }

  .header__nav-link {
    position: relative;
    font-size: 2rem;
    font-weight: 700;
    text-align: center;
    transition: letter-spacing 0.25s;
  }

  .header__nav-link:is(:hover, :focus) {
    letter-spacing: 0.25rem;
  }

  .header__nav-link::after {
    content: '';
    z-index: -1;
    position: absolute;
    left: -0.5rem;
    bottom: 0;
    width: 0;
    height: 50%;
    background-image: linear-gradient(
      to right,
      rgba(var(--primary-color-rgb), 0.2) 50%,
      rgba(var(--secondary-color-rgb), 0.2) 50%
    );
    transition: width 0.25s;
  }

  .header__nav-link:is(:hover, :focus)::after {
    width: calc(100% + 1rem);
  }
}

@media (width >= 768px) {
  .header__nav {
    grid-area: 1 / 1;
    height: 100%;
    display: flex;
    align-items: center;
  }

  .header__nav-list {
    display: flex;
    gap: 1rem;
  }

  .header__nav-link {
    display: inline-block;
    width: 5rem;
    padding-block: 0.5rem;
    font-size: 1.05rem;
    font-weight: 600;
    text-align: center;
    text-decoration: 1px underline wavy transparent;
    text-underline-offset: 0.25rem;
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-image: linear-gradient(to right, var(--text-color), var(--text-color));
    transition: text-decoration-color 0.25s;
  }

  .header__nav-link:hover {
    text-decoration-color: rgba(var(--primary-color-rgb), 0.25);
    background-image: linear-gradient(
      to right,
      var(--primary-color) 50%,
      var(--secondary-color) 50%
    );
  }

  .header__nav-link--separated {
    margin-right: 5rem;
  }
}
</style>
