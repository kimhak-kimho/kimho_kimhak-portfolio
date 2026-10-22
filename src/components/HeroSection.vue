<template>
  <section id="overview" class="hero section" :class="{ 'is-loaded': isLoaded }">
    <div class="hero-bg" aria-hidden="true">
      <div class="hero-wash"></div>
      <div class="hero-grid"></div>
    </div>

    <div class="container hero-grid-layout">
      <div class="hero-copy">
        <p class="hero-role hero-animate">Data Coordinator · Insights &amp; Reporting</p>

        <h1 class="hero-title hero-animate">
          <span class="hero-greeting">Hey! I'm</span>
          <span class="hero-name">KIMHAK</span>
        </h1>

        <p class="hero-summary hero-animate">
          Turning student and academic data into clear reports that support better decisions.
        </p>

        <div class="hero-cta hero-animate">
          <a class="btn btn-primary" href="#projects">Learn More</a>
          <a class="btn btn-secondary" href="#contact">Hire Me</a>
        </div>
      </div>

      <aside class="hero-side hero-animate-side">
        <div class="avatar-stage">
          <div class="avatar-wrap">
            <img :src="profileImage" alt="Kimhak profile photo" class="avatar" />
          </div>
        </div>
      </aside>
    </div>

    <Highlights class="hero-animate" />
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import profileImage from '../assets/profile2026.jpg'
import Highlights from './Highlights.vue'

const isLoaded = ref(false)

onMounted(() => {
  requestAnimationFrame(() => {
    isLoaded.value = true
  })
})
</script>

<style scoped>
.hero {
  position: relative;
  padding: 2.75rem 0 1.75rem;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}

.hero-wash {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse 55% 55% at 78% 42%, rgba(77, 163, 255, 0.14), transparent 62%),
    radial-gradient(ellipse 45% 40% at 12% 70%, rgba(45, 212, 191, 0.07), transparent 58%);
}

.hero-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(148, 180, 210, 0.06) 1px, transparent 1px),
    linear-gradient(90deg, rgba(148, 180, 210, 0.05) 1px, transparent 1px);
  background-size: 56px 56px;
  mask-image: radial-gradient(ellipse 70% 60% at 50% 40%, #000 10%, transparent 72%);
  opacity: 0.45;
}

.hero-grid-layout {
  position: relative;
  z-index: 1;
  width: min(1180px, calc(100% - 2rem));
  display: grid;
  grid-template-columns: minmax(300px, 1.05fr) minmax(280px, 0.9fr);
  gap: clamp(1.25rem, 3vw, 2rem);
  align-items: center;
}

.hero-copy {
  max-width: 36rem;
  display: flex;
  flex-direction: column;
  gap: 0;
  justify-content: center;
}

.hero-role {
  margin: 0 0 0.85rem;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--primary-2);
}

.hero-title {
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
  line-height: 1.05;
}

.hero-greeting {
  font-size: clamp(1.15rem, 2.4vw, 1.45rem);
  font-weight: 600;
  color: var(--muted);
  letter-spacing: 0.01em;
}

.hero-name {
  font-size: clamp(2.8rem, 6vw, 4.4rem);
  font-weight: 800;
  letter-spacing: -0.03em;
  color: var(--text);
  background: linear-gradient(135deg, #e8eef6 10%, var(--primary-2) 55%, #4da3ff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-summary {
  margin: 1.15rem 0 0;
  max-width: 32rem;
  font-size: 1.05rem;
  line-height: 1.7;
  color: var(--muted);
}

.hero-cta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.85rem;
  margin-top: 1.75rem;
}

.hero-side {
  display: flex;
  justify-content: center;
  justify-self: end;
  width: 100%;
  max-width: 360px;
}

.avatar-stage {
  animation: avatarFloat 7s ease-in-out infinite;
}

.avatar-wrap {
  width: min(300px, 100%);
  aspect-ratio: 1;
  border-radius: 50%;
  padding: 5px;
  background: linear-gradient(145deg, rgba(107, 196, 255, 0.55), rgba(45, 212, 191, 0.25));
  box-shadow: 0 18px 40px rgba(2, 8, 20, 0.35);
  animation: avatarPulse 5s ease-in-out infinite;
}

.avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  display: block;
  border: 3px solid rgba(8, 15, 31, 0.85);
}

.hero-animate,
.hero-animate-side {
  opacity: 0;
}

.hero-animate {
  transform: translateY(18px);
}

.hero-animate-side {
  transform: translateX(20px);
}

.hero.is-loaded .hero-animate,
.hero.is-loaded :deep(.hero-highlights.hero-animate) {
  animation: fadeUp 0.7s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.hero.is-loaded .hero-role { animation-delay: 0.05s; }
.hero.is-loaded .hero-title { animation-delay: 0.15s; }
.hero.is-loaded .hero-summary { animation-delay: 0.28s; }
.hero.is-loaded .hero-cta { animation-delay: 0.4s; }
.hero.is-loaded :deep(.hero-highlights.hero-animate) { animation-delay: 0.5s; }

.hero :deep(.hero-highlights.hero-animate) {
  opacity: 0;
  transform: translateY(18px);
}

.hero.is-loaded .hero-animate-side {
  animation: fadeIn 0.8s cubic-bezier(0.22, 1, 0.36, 1) 0.2s forwards;
}

@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeIn {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes avatarFloat {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

@keyframes avatarPulse {
  0%, 100% {
    box-shadow:
      0 18px 40px rgba(2, 8, 20, 0.35),
      0 0 0 0 rgba(77, 163, 255, 0.2);
  }
  50% {
    box-shadow:
      0 22px 48px rgba(2, 8, 20, 0.4),
      0 0 0 10px rgba(77, 163, 255, 0.08);
  }
}

@media (prefers-reduced-motion: reduce) {
  .hero-animate,
  .hero-animate-side,
  .avatar-stage,
  .avatar-wrap {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}

@media (max-width: 900px) {
  .hero {
    padding: 2.5rem 0 3.5rem;
  }

  .hero-grid-layout {
    grid-template-columns: 1fr;
    gap: 2rem;
    text-align: center;
  }

  .hero-copy {
    max-width: 36rem;
    margin: 0 auto;
    align-items: center;
  }

  .hero-summary {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-cta {
    justify-content: center;
  }

  .hero-side {
    order: -1;
    margin-left: auto;
    margin-right: auto;
    justify-self: center;
  }

  .avatar-wrap {
    width: min(240px, 68vw);
  }
}

@media (max-width: 480px) {
  .hero-name {
    font-size: clamp(2.3rem, 11vw, 2.8rem);
  }

  .hero-summary {
    font-size: 0.95rem;
  }

  .hero-cta {
    width: 100%;
    flex-direction: column;
  }

  .hero-cta .btn {
    width: 100%;
  }

  .avatar-wrap {
    width: min(200px, 64vw);
  }
}
</style>
