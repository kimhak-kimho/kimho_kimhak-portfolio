<template>
  <section id="education" class="section">
    <div class="container">
      <div class="section-head" data-reveal>
        <h2 class="title">Education</h2>
        <p class="subtitle">Academic journey supported by MoEYS, USAID, and EU scholarships</p>
        <div class="section-divider"></div>
      </div>

      <div class="scholarship-progress card" data-reveal>
        <h3 class="block-title">Scholarship Progression</h3>
        <div class="progression-track">
          <a
            v-for="(step, stepIndex) in scholarshipProgress"
            :key="step.sponsor"
            class="progression-step"
            :href="step.url"
            target="_blank"
            rel="noopener noreferrer"
          >
            <div class="step-node">
              <span
                class="step-dot"
                :class="{ 'is-active': stepIndex === scholarshipProgress.length - 1 }"
              ></span>
              <span
                v-if="stepIndex < scholarshipProgress.length - 1"
                class="step-line"
              ></span>
            </div>
            <div class="step-content">
              <strong>{{ step.sponsor }}</strong>
              <span>{{ step.program }}</span>
              <span class="step-period">{{ step.period }}</span>
            </div>
          </a>
        </div>
      </div>

      <div class="timeline">
        <article
          v-for="(item, index) in items"
          :key="`${item.school}-${item.program || item.year}`"
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
              <p v-if="item.address" class="address">
                <v-icon icon="mdi-map-marker-outline" size="16" />
                {{ item.address }}
              </p>
              <p v-if="item.program" class="program">
                <v-icon icon="mdi-school-outline" size="16" />
                {{ item.program }}
              </p>
              <p v-if="item.detail" class="detail">{{ item.detail }}</p>
              <p v-if="item.scholarship" class="scholarship">
                <v-icon icon="mdi-medal-outline" size="16" />
                {{ item.scholarship }}
              </p>
              <div v-if="item.documents?.length" class="doc-actions">
                <a
                  v-for="doc in item.documents"
                  :key="doc.url"
                  class="doc-btn"
                  :class="doc.primary ? 'doc-btn-primary' : 'doc-btn-outline'"
                  :href="doc.url"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  <v-icon :icon="doc.icon" size="16" />
                  {{ doc.label }}
                  <v-icon icon="mdi-open-in-new" size="14" />
                </a>
              </div>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
const scholarshipProgress = [
  {
    sponsor: 'MoEYS',
    program: 'Finance and Banking',
    period: '2022 – 2023',
    url: 'https://web.facebook.com/share/1AAnK3MwuA/',
  },
  {
    sponsor: 'USAID',
    program: 'Information Technology',
    period: '2023 – 2026',
    url: 'https://web.facebook.com/share/p/1DnAqMuvbH/',
  },
  {
    sponsor: 'EU',
    program: 'Management Information Systems',
    period: '2026 – 2028',
    url: 'https://web.facebook.com/share/18cq6gJVeF/',
  },
]

const items = [
  {
    school: 'National University of Battambang',
    program: 'Master’s Degree in Management Information Systems',
    period: '2026 – 2028',
    year: '2026',
    detail: 'Start: 07 November 2026',
    scholarship: 'Scholarship by EU',
    isCurrent: false,
    documents: [
      {
        label: 'Scholarship (EU)',
        url: 'https://web.facebook.com/share/18cq6gJVeF/',
        icon: 'mdi-medal-outline',
        primary: false,
      },
    ],
  },
  {
    school: 'National University of Battambang',
    program: 'Bachelor’s Degree in Information Technology',
    period: '2023 – 2026',
    year: '2023',
    detail: 'Graduated: 25 July 2026',
    scholarship: 'Scholarship by USAID',
    isCurrent: false,
    documents: [
      {
        label: 'View Transcript',
        url: 'https://verify.nubb.edu.kh/verified/021e44a0-bdc3-492b-b6f7-b04bc371e7ce',
        icon: 'mdi-file-document-outline',
        primary: true,
      },
      {
        label: 'Temporary Certificate',
        url: 'https://verify.nubb.edu.kh/verified/9d4c7f27-45cd-4959-8683-d76b0b8aec8a',
        icon: 'mdi-certificate-outline',
        primary: false,
      },
      {
        label: 'Scholarship (USAID)',
        url: 'https://web.facebook.com/share/p/1DnAqMuvbH/',
        icon: 'mdi-medal-outline',
        primary: false,
      },
    ],
  },
  {
    school: 'National University of Battambang',
    program: 'Bachelor’s Degree in Finance and Banking',
    period: '2022 – 2023',
    year: '2021',
    detail: 'Completed two years of coursework',
    scholarship: 'Scholarship by MoEYS',
    isCurrent: false,
    documents: [
      {
        label: 'View Transcript',
        url: 'https://verify.nubb.edu.kh/verified/f40b0551-c709-457c-869c-e4308fc1f69d',
        icon: 'mdi-file-document-outline',
        primary: true,
      },
      {
        label: 'Scholarship (MoEYS)',
        url: 'https://web.facebook.com/share/1AAnK3MwuA/',
        icon: 'mdi-medal-outline',
        primary: false,
      },
    ],
  },
  
  {
    school: 'Rongko Highschool',
    program: null,
    period: '2018 – 2021',
    year: '2018',
    address: 'Mongkol Borey district, Banteay Meanchey Province',
    detail: null,
    isCurrent: false,
  },
  {
    school: 'Soeur Secondary School',
    program: null,
    period: '2015 – 2018',
    year: '2015',
    address: 'Mongkol Borey district, Banteay Meanchey Province',
    detail: null,
    isCurrent: false,
  },
]
</script>

<style scoped>
.scholarship-progress {
  padding: 1.35rem 1.5rem 1.5rem;
  margin-bottom: 2rem;
  border-top: 3px solid rgba(77, 163, 255, 0.45);
}

.block-title {
  margin: 0 0 1.1rem;
  font-size: 0.95rem;
  font-weight: 700;
  font-style: italic;
  color: var(--text);
}

.progression-track {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 0.75rem;
}

.progression-step {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 0.75rem;
  text-decoration: none;
  color: inherit;
  border-radius: 12px;
  padding: 0.35rem;
  transition: background 0.2s ease;
}

.progression-step:hover {
  background: rgba(77, 163, 255, 0.06);
}

.step-node {
  display: flex;
  align-items: center;
  width: 100%;
  position: relative;
}

.step-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--surface-2);
  border: 2px solid rgba(77, 163, 255, 0.45);
  flex-shrink: 0;
  z-index: 1;
}

.step-dot.is-active {
  background: linear-gradient(135deg, var(--primary), var(--primary-2));
  border-color: var(--primary-2);
  box-shadow: 0 0 12px rgba(77, 163, 255, 0.4);
}

.step-line {
  flex: 1;
  height: 2px;
  margin-left: 0.35rem;
  background: linear-gradient(to right, var(--primary), rgba(77, 163, 255, 0.2));
}

.step-content {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  font-size: 0.85rem;
  color: var(--muted);
  line-height: 1.45;
}

.step-content strong {
  color: var(--text);
  font-size: 0.95rem;
}

.step-period {
  font-size: 0.78rem;
  opacity: 0.85;
}

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

.address {
  margin: 0.35rem 0 0;
  display: flex;
  align-items: flex-start;
  gap: 0.45rem;
  color: var(--muted);
  font-size: 0.92rem;
  line-height: 1.45;
}

.address :deep(.v-icon) {
  color: var(--primary);
  flex-shrink: 0;
  margin-top: 0.1rem;
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

.scholarship {
  margin: 0.45rem 0 0;
  display: flex;
  align-items: center;
  gap: 0.4rem;
  color: var(--primary-2);
  font-size: 0.9rem;
  font-weight: 600;
}

.scholarship :deep(.v-icon) {
  color: var(--primary);
}

.doc-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.65rem;
  margin-top: 1rem;
}

.doc-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  width: fit-content;
  padding: 0.5rem 0.85rem;
  border-radius: 10px;
  font-size: 0.82rem;
  font-weight: 600;
  line-height: 1;
  text-decoration: none;
  transition: background 0.2s ease, border-color 0.2s ease, color 0.2s ease;
}

.doc-btn-primary {
  background: linear-gradient(135deg, var(--primary), #3b8fd9);
  color: #061018;
  border: 1px solid transparent;
}

.doc-btn-primary:hover {
  filter: brightness(1.06);
}

.doc-btn-outline {
  background: transparent;
  color: var(--primary-2);
  border: 1px solid var(--border);
}

.doc-btn-outline:hover {
  border-color: var(--border-strong);
  background: rgba(77, 163, 255, 0.08);
}

@media (max-width: 768px) {
  .progression-track {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .progression-step {
    flex-direction: row;
    text-align: left;
    align-items: flex-start;
  }

  .step-node {
    width: auto;
    flex-direction: column;
    align-items: center;
    padding-top: 0.2rem;
  }

  .step-line {
    width: 2px;
    height: 100%;
    min-height: 28px;
    margin: 0.35rem 0 0;
    background: linear-gradient(to bottom, var(--primary), rgba(77, 163, 255, 0.2));
  }

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
