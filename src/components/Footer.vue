<template>
  <footer class="footer">
    <div class="container wrap">
      <p>© {{ year }} kimho kimhak - Data Analyst </p>
      <div class="socials">
        <a href="https://www.facebook.com/kimho.kimhak/" target="_blank" rel="noopener noreferrer" aria-label="Facebook">
          <span>Facebook</span>
        </a>
        <a
          href="https://www.linkedin.com/in/kimhak-kimho-7621b6266/"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="LinkedIn"
        >
          <span>LinkedIn</span>
        </a>
        <a href="https://t.me/Kimho_Kimhak" target="_blank" rel="noopener noreferrer" aria-label="Telegram">
          <span>Telegram</span>
        </a>
      </div>
    </div>
  </footer>
</template>

<script setup>
const year = new Date().getFullYear()
</script>

<style scoped>
.footer {
  border-top: 1px solid var(--border);
  padding: 2rem 0;
  margin-top: 1rem;
}

.wrap {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

p {
  margin: 0;
  color: var(--muted);
  font-size: 0.88rem;
}

.socials {
  display: flex;
  gap: 0.5rem;
}

.socials a {
  min-width: 84px;
  height: 34px;
  padding: 0 0.55rem;
  display: grid;
  place-items: center;
  border: 1px solid var(--border);
  border-radius: 12px;
  color: var(--text);
  transition: all 0.3s ease;
  text-decoration: none;
}

.socials span {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.socials a:hover {
  color: var(--primary-2);
  border-color: var(--border-strong);
  transform: translateY(-2px);
}

@media (max-width: 640px) {
  .wrap {
    flex-direction: column;
    text-align: center;
  }

  .socials {
    width: 100%;
    justify-content: center;
    flex-wrap: wrap;
  }
}

@media (max-width: 480px) {
  .footer {
    padding: 1.5rem 0;
  }

  .socials a {
    flex: 1 1 calc(50% - 0.25rem);
    min-width: 0;
  }
}
</style>
