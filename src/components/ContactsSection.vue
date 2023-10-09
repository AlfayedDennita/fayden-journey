<script setup>
import { ref, computed } from 'vue';

import JourneySection from './JourneySection.vue';

const formData = ref({
  name: '',
  email: '',
  message: '',
});
const formStatus = ref('idle'); // ['idle', 'sending', 'sent', 'failed']

const formStatusText = computed(() => {
  let text;

  switch (formStatus.value) {
    case 'sending':
      text = 'Sending...';
      break;
    case 'sent':
      text = 'Sent successfully!';
      break;
    case 'failed':
      text = 'Something went wrong. Failed to send.';
      break;
  }

  return text;
});

async function submitFormHandler() {
  try {
    formStatus.value = 'sending';

    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json',
      },
      body: JSON.stringify({
        access_key: '459e9b6c-ad8a-4594-b414-b960b520fbee',
        subject: 'Fayden Journey Contact Form',
        from_name: 'Fayden Journey',
        name: formData.value.name,
        email: formData.value.email,
        message: formData.value.message,
      }),
    });

    const result = await response.json();

    if (result.success) {
      formStatus.value = 'sent';
    } else {
      throw new Error();
    }
  } catch (error) {
    console.log(error);
    formStatus.value = 'failed';
  }
}

const socials = [
  {
    name: 'Facebook',
    iconClass: 'fab fa-facebook',
    url: 'https://www.facebook.com/AlfayedDennita',
  },
  {
    name: 'Instagram',
    iconClass: 'fab fa-instagram',
    url: 'https://www.instagram.com/alfayeddennita',
  },
  {
    name: 'GitHub',
    iconClass: 'fab fa-github',
    url: 'https://github.com/AlfayedDennita',
  },
  {
    name: 'LinkedIn',
    iconClass: 'fab fa-linkedin',
    url: 'https://www.linkedin.com/in/alfayeddennita',
  },
];
</script>

<template>
  <JourneySection
    id="contacts"
    title="Keep Connecting"
    icon-class="fas fa-link"
    icon-color-variant="secondary"
    description="We have arrived at the end, so keep in touch with me through this way."
  >
    <div class="contacts-section__content">
      <form class="contacts-section__form" method="post" @submit.prevent="submitFormHandler">
        <header class="contacts-section__form-header">
          <h3 class="contacts-section__form-title">Send a Message</h3>
        </header>
        <div class="contacts-section__form-inputs">
          <div class="contacts-section__form-input-group" title="Name">
            <label class="contacts-section__form-label" for="contact-form-name">Name</label>
            <input
              v-model="formData.name"
              class="contacts-section__form-input"
              id="contact-form-name"
              type="text"
              :disabled="formStatus === 'sending'"
              required
            />
          </div>
          <div class="contacts-section__form-input-group" title="Email">
            <label class="contacts-section__form-label" for="contact-form-email">Email</label>
            <input
              v-model="formData.email"
              class="contacts-section__form-input"
              id="contact-form-email"
              type="email"
              :disabled="formStatus === 'sending'"
              required
            />
          </div>
          <div
            class="contacts-section__form-input-group contacts-section__form-input-group--message"
            title="Message"
          >
            <label class="contacts-section__form-label" for="contact-form-message">Message</label>
            <textarea
              v-model="formData.message"
              class="contacts-section__form-input contacts-section__form-input--message"
              id="contact-form-message"
              :disabled="formStatus === 'sending'"
              required
            />
          </div>
        </div>
        <footer class="contacts-section__form-footer">
          <button
            class="contacts-section__form-submit-button"
            type="submit"
            title="Submit"
            :disabled="formStatus === 'sending'"
          >
            Submit
          </button>
          <div
            v-if="formStatus && formStatus !== 'idle'"
            class="contacts-section__form-status"
            :class="{
              'contacts-section__form-status--success': formStatus === 'sent',
              'contacts-section__form-status--failed': formStatus === 'failed',
            }"
          >
            <i
              v-if="formStatus === 'sending'"
              class="fas fa-spinner fa-spin contacts-section__form-status-icon"
            />
            <i
              v-else-if="formStatus === 'sent'"
              class="fas fa-check contacts-section__form-status-icon"
            />
            <i
              v-else-if="formStatus === 'failed'"
              class="fas fa-xmark contacts-section__form-status-icon"
            />
            <p class="contacts-section__form-status-text">{{ formStatusText }}</p>
          </div>
        </footer>
      </form>

      <section class="contacts-section__socials">
        <header class="contacts-section__socials-header">
          <h3 class="contacts-section__socials-title">Social Channels</h3>
          <p class="contacts-section__socials-description">
            Check out my social media accounts here.
          </p>
        </header>
        <ul class="no-list contacts-section__socials-list">
          <li v-for="social in socials" :key="social.name">
            <a
              class="contacts-section__socials-link"
              :href="social.url"
              target="_blank"
              rel="external"
              :title="social.name"
            >
              <i :class="social.iconClass" />
            </a>
          </li>
        </ul>
      </section>
    </div>

    <img
      class="contacts-section__decoration"
      src="https://storage.googleapis.com/fayden-journey/images/decorations/blue-diamonds.svg"
      alt=""
    />
  </JourneySection>
</template>

<style scoped>
.contacts-section__content {
  display: grid;
  gap: 3rem;
}

@media (width >= 768px) {
  .contacts-section__content {
    grid-template-columns: 6fr 4fr;
  }
}

.contacts-section__form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.contacts-section__form-title {
  font-family: var(--heading-font-family);
  font-size: 1.25rem;
  font-weight: 500;
}

.contacts-section__form-inputs {
  display: grid;
  gap: 0.75rem;
}

@media (width >= 768px) {
  .contacts-section__form-inputs {
    grid-template-columns: repeat(2, 1fr);
  }
}

.contacts-section__form-input-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.contacts-section__form-label {
  font-size: 0.9rem;
  font-weight: 500;
}

.contacts-section__form-input {
  padding: 0.75rem 1.25rem;
  background-color: var(--gray-1);
  border-radius: 0.25rem;
  transition: background-color 0.5s;
}

.contacts-section__form-input:focus {
  background-color: var(--gray-2);
}

.contacts-section__form-input--message {
  height: 10rem;
}

@media (width >= 768px) {
  .contacts-section__form-input-group--message {
    grid-column: 1 / 3;
  }

  .contacts-section__form-input--message {
    height: 12.5rem;
  }
}

.contacts-section__form-footer {
  justify-self: start;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 1rem;
}

.contacts-section__form-submit-button {
  padding: 0.75rem 2rem;
  background-color: var(--primary-color);
  border-radius: 0.25rem;
  font-weight: 500;
  color: var(--bg-color);
  transition: background-color 0.25s;
}

.contacts-section__form-submit-button:is(:hover, :focus) {
  background-color: rgba(var(--primary-color-rgb), 0.9);
}

.contacts-section__form-submit-button:disabled {
  background-color: rgba(var(--primary-color-rgb), 0.5);
}

.contacts-section__form-status {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.contacts-section__form-status--success {
  color: var(--green);
}

.contacts-section__form-status--failed {
  color: var(--red);
}

.contacts-section__socials {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.contacts-section__socials-header {
  display: flex;
  flex-direction: column;
}

.contacts-section__socials-title {
  font-family: var(--heading-font-family);
  font-size: 1.25rem;
  font-weight: 500;
}

.contacts-section__socials-description {
  font-size: 0.9rem;
}

.contacts-section__socials-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.contacts-section__socials-link {
  width: 2.5rem;
  height: 2.5rem;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  background-color: var(--gray-1);
  border-radius: 50%;
  font-size: 1.25rem;
  transition: background-color 0.25s;
}

.contacts-section__socials-link:is(:hover, :focus) {
  background-color: var(--gray-2);
}

.contacts-section__decoration {
  z-index: -1;
  position: absolute;
  inset: 30% -15rem auto auto;
  width: 20rem;
  height: 20rem;
  rotate: 45deg;
  opacity: 0.05;
}
</style>
