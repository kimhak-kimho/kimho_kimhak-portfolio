<template>
  <div
    class="hero-highlights"
    @mouseenter="pause"
    @mouseleave="resume"
    @focusin="pause"
    @focusout="resume"
  >
    <div class="highlights-label">
      <span>Highlights</span>
      <p>Training, certifications, and data work</p>
    </div>

    <div class="carousel">
      <div class="carousel-viewport">
        <div
          class="carousel-track"
          :style="{
            '--visible': visibleCount,
            transform: `translateX(-${active * slidePercent}%)`,
          }"
        >
          <figure
            v-for="item in highlights"
            :key="item.title"
            class="highlight-card"
          >
            <img :src="item.src" :alt="item.alt" />
            <figcaption>
              <strong>{{ item.title }}</strong>
              <span>{{ item.description }}</span>
            </figcaption>
          </figure>
        </div>
      </div>

      <div class="carousel-controls">
        <button
          type="button"
          class="carousel-btn"
          aria-label="Previous highlight"
          @click="prev"
        >
          <v-icon icon="mdi-chevron-left" size="20" />
        </button>

        <div class="carousel-dots" role="tablist" aria-label="Highlight slides">
          <button
            v-for="(_, index) in maxIndex + 1"
            :key="index"
            type="button"
            class="dot"
            role="tab"
            :class="{ active: active === index }"
            :aria-label="`Go to slide ${index + 1}`"
            :aria-selected="active === index"
            @click="goTo(index)"
          />
        </div>

        <button
          type="button"
          class="carousel-btn"
          aria-label="Next highlight"
          @click="next"
        >
          <v-icon icon="mdi-chevron-right" size="20" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue'

import photoAws from '../assets/photosSlide/photo_2026-10-21_19-21-11.jpg'
import photoField from '../assets/photosSlide/photo_2026-10-21_19-21-12.jpg'
import photoCommunity from '../assets/photosSlide/photo_2026-10-21_19-21-13.jpg'
import photoDashboard from '../assets/photosSlide/photo_2026-10-21_19-21-14.jpg'
import photoCohort from '../assets/photosSlide/photo_2026-10-21_19-21-15.jpg'
import photoIctWorkshop from '../assets/photosSlide/photo_2026-10-21_19-21-16.jpg'
import photoCapstone from '../assets/photosSlide/photo_2026-10-21_19-21-17.jpg'
import photoDataWorkshop from '../assets/photosSlide/photo_2026-10-06_21-53-03.jpg'

const INTERVAL_MS = 3000

const highlights = [
  {
    src: photoAws,
    alt: 'AWS Academy certificate ceremony',
    title: 'AWS Academy',
    description: 'Certificate of Completion from AWS Academy training.',
  },
  {
    src: photoDataWorkshop,
    alt: 'Data analytics workshop group photo',
    title: 'Data Analytics',
    description: 'Built dashboards with Google Looker Studio.',
  },
  {
    src: photoDashboard,
    alt: 'Presenting an ASEAN statistical dashboard',
    title: 'Dashboard Presentation',
    description: 'Presented analytical charts in class.',
  },
  {
    src: photoIctWorkshop,
    alt: 'ICT Edge career readiness workshop certificate',
    title: 'ICT Skills Workshop',
    description: 'Asia Foundation ICT Edge skills workshop.',
  },
  {
    src: photoCapstone,
    alt: 'Smart library management system project defense',
    title: 'Project Defense',
    description: 'Smart Library System with RFID and QR.',
  },
  {
    src: photoCohort,
    alt: 'Training cohort with certificates',
    title: 'Training Cohort',
    description: 'Completed a skills development program.',
  },
  {
    src: photoCommunity,
    alt: 'University community event group photo',
    title: 'Community Event',
    description: 'University and partner collaboration events.',
  },
  {
    src: photoField,
    alt: 'Field visit group photo at border checkpoint',
    title: 'Field Engagement',
    description: 'Institutional and field engagement activities.',
  },
]

const active = ref(0)
const visibleCount = ref(4)
let timer = null

const slidePercent = computed(() => 100 / visibleCount.value)
const maxIndex = computed(() =>
  Math.max(0, highlights.length - visibleCount.value)
)

const updateVisibleCount = () => {
  const width = window.innerWidth
  if (width <= 480) visibleCount.value = 1
  else if (width <= 720) visibleCount.value = 2
  else if (width <= 1000) visibleCount.value = 3
  else visibleCount.value = 4

  if (active.value > maxIndex.value) {
    active.value = maxIndex.value
  }
}

const next = () => {
  active.value = active.value >= maxIndex.value ? 0 : active.value + 1
}

const prev = () => {
  active.value = active.value <= 0 ? maxIndex.value : active.value - 1
}

const goTo = (index) => {
  active.value = Math.min(index, maxIndex.value)
}

const start = () => {
  stop()
  timer = window.setInterval(next, INTERVAL_MS)
}

const stop = () => {
  if (timer) {
    clearInterval(timer)
    timer = null
  }
}

const pause = () => stop()
const resume = () => start()

onMounted(() => {
  updateVisibleCount()
  window.addEventListener('resize', updateVisibleCount)
  const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)')
  if (!prefersReduced.matches) start()
})

onUnmounted(() => {
  stop()
  window.removeEventListener('resize', updateVisibleCount)
})
</script>

<style scoped>
.hero-highlights {
  width: min(1180px, calc(100% - 2rem));
  margin: 1.5rem auto 0;
  position: relative;
  z-index: 1;
}

.highlights-label {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 0.55rem 1rem;
  margin-bottom: 0.85rem;
}

.highlights-label span {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--primary-2);
}

.highlights-label p {
  margin: 0;
  font-size: 0.9rem;
  color: var(--muted);
}

.carousel {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.carousel-viewport {
  overflow: hidden;
  width: 100%;
}

.carousel-track {
  display: flex;
  width: 100%;
  transition: transform 0.55s cubic-bezier(0.22, 1, 0.36, 1);
  will-change: transform;
}

.highlight-card {
  flex: 0 0 calc(100% / var(--visible, 4));
  width: calc(100% / var(--visible, 4));
  min-width: 0;
  margin: 0;
  padding: 0 0.4rem;
  box-sizing: border-box;
}

.highlight-card img {
  width: 100%;
  aspect-ratio: 16 / 10;
  object-fit: cover;
  display: block;
  border-radius: 12px 12px 0 0;
  border: 1px solid var(--border);
  border-bottom: none;
  background: rgba(9, 18, 38, 0.45);
  transition: transform 0.3s ease;
}

.highlight-card:hover img {
  transform: scale(1.03);
}

.highlight-card figcaption {
  padding: 0.55rem 0.65rem 0.7rem;
  font-size: 0.75rem;
  color: var(--muted);
  line-height: 1.4;
  border: 1px solid var(--border);
  border-top: none;
  border-radius: 0 0 12px 12px;
  background: rgba(9, 18, 38, 0.55);
}

.highlight-card figcaption strong {
  display: block;
  color: var(--text);
  font-size: 0.82rem;
  margin-bottom: 0.15rem;
}

.highlight-card figcaption span {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.carousel-controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
}

.carousel-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  border-radius: 999px;
  border: 1px solid var(--border);
  background: rgba(9, 18, 38, 0.55);
  color: var(--text);
  cursor: pointer;
  transition: border-color 0.2s ease, background 0.2s ease;
}

.carousel-btn:hover {
  border-color: rgba(77, 163, 255, 0.55);
  background: rgba(77, 163, 255, 0.12);
}

.carousel-dots {
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.dot {
  width: 0.5rem;
  height: 0.5rem;
  padding: 0;
  border: none;
  border-radius: 999px;
  background: rgba(148, 180, 210, 0.35);
  cursor: pointer;
  transition: width 0.2s ease, background 0.2s ease;
}

.dot.active {
  width: 1.2rem;
  background: var(--primary-2);
}

@media (max-width: 480px) {
  .hero-highlights {
    margin-top: 1.25rem;
  }

  .highlight-card {
    padding: 0;
  }
}

@media (prefers-reduced-motion: reduce) {
  .carousel-track {
    transition: none;
  }
}
</style>
