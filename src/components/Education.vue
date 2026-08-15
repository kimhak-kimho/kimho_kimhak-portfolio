<template>
  <section id="education" class="section">
    <div class="container">
      <div class="section-head" data-reveal>
        <h2 class="title">Education</h2>
        <p class="subtitle">Academic journey from secondary school to information technology studies</p>
        <div class="section-divider"></div>
      </div>

      <div class="timeline">
        <article
          v-for="(item, index) in items"
          :key="item.school"
          class="timeline-item"
          data-reveal
          :style="{ '--reveal-delay': `${index * 0.1}s` }"
        >
          <div class="timeline-marker">
            <span class="timeline-dot" :class="{ 'is-current': item.isCurrent }"></span>
            <span class="timeline-year">{{ item.year }}</span>
          </div>

          <div class="timeline-card card">
            <div class="entry-meta">
              <span v-if="item.isCurrent" class="current-badge">Current</span>
              <span class="period">{{ item.period }}</span>
            </div>

            <div class="entry-copy">
              <h3 class="school">{{ item.school }}</h3>
              <p v-if="item.program" class="program">
                <v-icon icon="mdi-school-outline" size="16" />
                {{ item.program }}
              </p>
              <p v-if="item.detail" class="detail">{{ item.detail }}</p>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
const items = [
  {
    school: 'National University of Battambang',
    program: 'Information Technology',
    period: '2021 – Present',
    year: '2021',
    detail: 'Graduated: 25 July 2026',
    isCurrent: true,
  },
  {
    school: 'Rongko Highschool',
    program: null,
    period: '2018 – 2021',
    year: '2018',
    detail: null,
    isCurrent: false,
  },
  {
    school: 'Soeur Secondary School',
    program: null,
    period: '2015 – 2018',
    year: '2015',
    detail: null,
    isCurrent: false,
  },
]
</script>

<style scoped>
.timeline {
  width: 100%;
  position: relative;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 28px;
  top: 12px;
  bottom: 12px;
  width: 2px;
  background: linear-gradient(
    to bottom,
    var(--primary),
    var(--primary-2) 60%,
    rgba(77, 163, 255, 0.15)
  );
}

.timeline-item {
  display: grid;
  grid-template-columns: 56px 1fr;
  gap: 1.5rem;
  position: relative;
}

.timeline-item + .timeline-item {
  margin-top: 1.75rem;
}

.timeline-marker {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.65rem;
  padding-top: 0.35rem;
  z-index: 1;
}

.timeline-dot {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: var(--surface);
  border: 3px solid var(--primary);
  box-shadow: 0 0 0 4px rgba(77, 163, 255, 0.12);
  flex-shrink: 0;
}

.timeline-dot.is-current {
  background: linear-gradient(135deg, var(--primary), var(--primary-2));
  border-color: var(--primary-2);
  box-shadow: 0 0 18px rgba(77, 163, 255, 0.45);
}

.timeline-year {
  font-size: 0.82rem;
  font-weight: 700;
  color: var(--primary);
  letter-spacing: 0.04em;
  writing-mode: vertical-rl;
  transform: rotate(180deg);
}

.timeline-card {
  padding: 1.5rem 1.75rem;
  border-top: 3px solid rgba(77, 163, 255, 0.55);
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.timeline-card:hover {
  transform: translateX(6px);
  border-color: var(--border-strong);
  box-shadow: var(--shadow-lift);
}

.entry-meta {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.65rem;
  margin-bottom: 0.85rem;
}

.current-badge {
  display: inline-flex;
  align-items: center;
  padding: 0.3rem 0.7rem;
  border-radius: 999px;
  background: rgba(77, 163, 255, 0.14);
  border: 1px solid rgba(77, 163, 255, 0.35);
  color: var(--primary-2);
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

.period {
  font-style: italic;
  color: var(--muted);
  font-size: 0.92rem;
}

.entry-copy {
  min-width: 0;
}

.school {
  margin: 0 0 0.5rem;
  font-size: 1.25rem;
  font-weight: 700;
}

.program {
  margin: 0 0 0.35rem;
  display: flex;
  align-items: center;
  gap: 0.45rem;
  color: var(--primary-2);
  font-size: 0.95rem;
  font-weight: 600;
}

.program :deep(.v-icon) {
  color: var(--primary);
}

.detail {
  margin: 0;
  color: var(--muted);
  font-size: 0.92rem;
}

@media (max-width: 768px) {
  .timeline::before {
    left: 14px;
  }

  .timeline-item {
    grid-template-columns: 32px 1fr;
    gap: 1rem;
  }

  .timeline-year {
    display: none;
  }

  .timeline-card {
    padding: 1.25rem 1.1rem;
  }

  .timeline-card:hover {
    transform: none;
  }
}

@media (max-width: 480px) {
  .school {
    font-size: 1.05rem;
  }

  .timeline-card {
    padding: 1rem 0.9rem;
  }
}
</style>
