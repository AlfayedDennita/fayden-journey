<template>
  <footer class="footer">
    <div class="container footer__container">
      <p class="footer__text">
        Built with ❤️ by myself. Copyright &copy; {{ new Date().getFullYear() }}
      </p>
    </div>
  </footer>
</template>

<style scoped>
.footer__container {
  padding-block: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

@media (width >= 768px) {
  .footer__container {
    padding-top: 5rem;
  }
}

.footer__text {
  font-size: 0.9rem;
  text-align: center;
  color: rgba(var(--text-color-rgb), 0.9);
}
</style>
