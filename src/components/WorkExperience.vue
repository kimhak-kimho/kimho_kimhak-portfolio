<template>
  <section id="experience" class="section">
    <div class="container">
      <div class="section-head" data-reveal>
        <h2 class="title">Work Experience</h2>
        <p class="subtitle">
          Data-driven career progression with measurable impact and continuous growth
        </p>
        <div class="section-divider"></div>
      </div>

      <div class="timeline">
        <article
          v-for="(item, index) in items"
          :key="item.role"
          class="timeline-item"
          data-reveal
          :style="{ '--reveal-delay': `${index * 0.12}s` }"
        >
          <div class="timeline-marker">
            <span class="timeline-dot" :class="{ 'is-current': item.isCurrent }"></span>
            <span class="timeline-year">{{ item.year }}</span>
          </div>

          <div class="timeline-card card">
            <header class="entry-header">
              <div class="entry-meta">
                <span v-if="item.isCurrent" class="current-badge">Current Role</span>
                <span class="period">{{ item.period }}</span>
              </div>
              <div class="entry-copy">
                <h3 class="role">{{ item.role }}</h3>
                <p class="company">
                  <v-icon icon="mdi-domain" size="16" />
                  {{ item.company }}
                </p>
              </div>
            </header>

            <div v-if="item.progression?.length" class="entry-block">
              <h4 class="block-title">Career Progression</h4>
              <div class="progression-track">
                <div
                  v-for="(step, stepIndex) in item.progression"
                  :key="step.title"
                  class="progression-step"
                >
                  <div class="step-node">
                    <span class="step-dot" :class="{ 'is-active': stepIndex === item.progression.length - 1 }"></span>
                    <span v-if="stepIndex < item.progression.length - 1" class="step-line"></span>
                  </div>
                  <div class="step-content">
                    <strong>{{ step.title }}</strong>
                    <span>{{ step.duration }}</span>
                  </div>
                </div>
              </div>
            </div>

            <div v-if="item.responsibilityGroups?.length" class="entry-block">
              <h4 class="block-title">Key Responsibilities</h4>
              <div class="responsibility-groups">
                <div
                  v-for="group in item.responsibilityGroups"
                  :key="group.title"
                  class="responsibility-group"
                >
                  <h5 class="group-title">
                    <v-icon :icon="group.icon" size="18" />
                    {{ group.title }}
                  </h5>
                  <ul>
                    <li v-for="point in group.items" :key="point">{{ point }}</li>
                  </ul>
                </div>
              </div>
            </div>

            <div v-else-if="item.responsibilities?.length" class="entry-block">
              <h4 class="block-title">Key Responsibilities</h4>
              <ul>
                <li v-for="point in item.responsibilities" :key="point">{{ point }}</li>
              </ul>
            </div>

            <div v-if="item.images?.length" class="entry-block">
              <h4 class="block-title">Work Highlights</h4>
              <p v-if="item.imagesDescription" class="block-description">{{ item.imagesDescription }}</p>
              <div class="entry-gallery">
                <figure v-for="photo in item.images" :key="photo.id" class="gallery-item">
                  <img :src="photo.src" :alt="photo.alt || item.role" />
                  <figcaption v-if="photo.title || photo.description">
                    <strong v-if="photo.title">{{ photo.title }}</strong>
                    <span v-if="photo.description">{{ photo.description }}</span>
                  </figcaption>
                </figure>
              </div>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
// 1. Put your image in src/assets/
// 2. Import it here
// 3. Add images to the item below
import workphoto01 from '../assets/Experience/workpho/workphoto01.jpg'
import workphoto02 from '../assets/Experience/workpho/workphoto02.jpg'
import workphoto05 from '../assets/Experience/workpho/workphoto05.jpg'
import workphoto06 from '../assets/Experience/workpho/workphoto06.jpg'
import workphoto10 from '../assets/Experience/workpho/myworkplace.jpg'

const workGallery = [
  {
    id: 1,
    src: workphoto01,
    alt: 'NUBB work experience photo 1',
    title: 'Graduate Record Verification',
    description: 'Coordinated with Verify.gov.kh',
  },
  {
    id: 2,
    src: workphoto02,
    alt: 'NUBB work experience photo 2',
    title: 'Student Enrollment Management',
    description: 'Managed and updated student enrollment data',
  },
  {
    id: 5,
    src: workphoto05,
    alt: 'NUBB work experience photo 5',
    title: 'Data Analysis Meeting',
    description: 'Analyzed enrollment and academic data with the team',
  },
  {
    id: 6,
    src: workphoto06,
    alt: 'NUBB work experience photo 6',
    title: 'Presentation',
    description: 'Presented analytical reports to university management',
  },
  {
    id: 10,
    src: workphoto10,
    alt: 'NUBB work experience photo 10',
    title: 'Database Management Office',
    description: 'Daily workplace for student data management and reporting',
  },
]

const items = [
  {
    role: 'Data Coordinator / Staff',
    company: 'National University of Battambang, Battambang',
    period: 'September 2023 – Present',
    year: '2023',
    isCurrent: true,
    images: workGallery,
    imagesDescription: 'Visual highlights from data operations, reporting, and day-to-day university work.',
    progression: [
      { title: 'Weekend Volunteer', duration: '1 year 3 months' },
      { title: 'Weekend Staff', duration: '9 months' },
      { title: 'Full-Time Staff', duration: 'Based on strong performance' },
    ],
    responsibilityGroups: [
  {
    title: 'Data Management',
    icon: 'mdi-database-outline',
    items: [
      'Managed and maintained student records for all academic levels in the University Management System',
      'Retrieved data using SQL (MySQL) for reporting, validation, and analysis',
      'Cleaned and validated data to ensure accuracy, consistency, and completeness',
      'Updated and maintained student records through regular data verification',
      'Managed student registration, transfers, major changes, and academic status updates',
    ],
  },
  {
    title: 'Data Analysis & Reporting',
    icon: 'mdi-chart-bar',
    items: [
      'Analyzed enrollment, GPA, and academic performance data to identify semester and yearly trends',
      'Prepared statistical reports, GPA reports, enrollment reports, and management summaries',
      'Created charts and dashboards using Excel, Python (Pandas, Matplotlib, Jupyter Notebook), and Power BI',
      'Developed reports and visualizations to support data-driven decision-making',
      'Presented analytical findings and key insights to university management',
    ],
  },
  {
    title: 'Database Operations',
    icon: 'mdi-cog-outline',
    items: [
      'Processed student data for enrollment, examinations, and academic records',
      'Validated examination results and maintained accurate transcripts and academic records',
      'Maintained and updated the student database to support daily university operations',
      'Improved data quality through regular validation and maintenance',
      'Supported academic reporting throughout each semester',
    ],
  },
  {
    title: 'Collaboration & Process Improvement',
    icon: 'mdi-account-group-outline',
    items: [
      'Worked with academic and administrative departments to resolve data and reporting issues',
      'Coordinated with Verify.gov.kh to verify graduate records and support degree certificate printing',
      'Provided accurate reports and statistical data to support university management',
      'Helped improve reporting processes and operational efficiency',
    ],
  },
],  
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
  margin-top: 2.5rem;
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
  padding: 1.75rem 2rem;
  border-top: 3px solid rgba(77, 163, 255, 0.55);
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.timeline-card:hover {
  transform: translateX(6px);
  border-color: var(--border-strong);
  box-shadow: var(--shadow-lift);
}

.entry-header {
  margin-bottom: 1.5rem;
}

.entry-copy {
  min-width: 0;
}

.entry-gallery {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 1rem;
}

.gallery-item {
  margin: 0;
  border-radius: 14px;
  overflow: hidden;
  border: 1px solid var(--border);
  background: rgba(9, 18, 38, 0.45);
}

.gallery-item img {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
  display: block;
  transition: transform 0.3s ease;
}

.gallery-item:hover img {
  transform: scale(1.04);
}

.gallery-item figcaption {
  padding: 0.65rem 0.75rem;
  font-size: 0.8rem;
  color: var(--muted);
  line-height: 1.45;
}

.gallery-item figcaption strong {
  display: block;
  color: var(--text);
  font-size: 0.82rem;
  margin-bottom: 0.15rem;
}

.entry-meta {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.65rem;
  margin-bottom: 0.75rem;
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

.role {
  margin: 0 0 0.5rem;
  font-size: 1.3rem;
  font-weight: 700;
}

.company {
  margin: 0;
  display: flex;
  align-items: center;
  gap: 0.45rem;
  color: var(--muted);
  font-size: 0.95rem;
}

.company :deep(.v-icon) {
  color: var(--primary);
}

.entry-block + .entry-block {
  margin-top: 1.5rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(255, 255, 255, 0.06);
}

.block-title {
  margin: 0 0 1rem;
  font-size: 0.95rem;
  font-weight: 700;
  font-style: italic;
  color: var(--text);
}

.block-description {
  margin: -0.5rem 0 1rem;
  color: var(--muted);
  font-size: 0.88rem;
  line-height: 1.6;
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
  gap: 0.25rem;
  font-size: 0.85rem;
  color: var(--muted);
  line-height: 1.5;
}

.step-content strong {
  color: var(--text);
  font-size: 0.9rem;
}

.responsibility-groups {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.responsibility-group {
  padding: 1rem 1.1rem;
  border-radius: 14px;
  border: 1px solid rgba(255, 255, 255, 0.06);
  background: rgba(9, 18, 38, 0.35);
}

.group-title {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin: 0 0 0.75rem;
  font-size: 0.92rem;
  font-weight: 700;
  color: var(--primary-2);
}

.group-title :deep(.v-icon) {
  color: var(--primary);
}

.responsibility-group ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.responsibility-group li {
  position: relative;
  padding-left: 1.1rem;
  margin-bottom: 0.5rem;
  color: var(--muted);
  line-height: 1.65;
  font-size: 0.92rem;
}

.responsibility-group li:last-child {
  margin-bottom: 0;
}

.responsibility-group li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.62rem;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--primary);
}

.entry-block ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.entry-block li {
  position: relative;
  padding-left: 1.1rem;
  margin-bottom: 0.55rem;
  color: var(--muted);
  line-height: 1.7;
}

.entry-block li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.65rem;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--primary);
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
    padding: 1.35rem 1.2rem;
  }

  .responsibility-groups {
    grid-template-columns: 1fr;
  }

  .entry-gallery {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

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

  .timeline-card:hover {
    transform: none;
  }
}

@media (max-width: 480px) {
  .role {
    font-size: 1.1rem;
  }

  .timeline-card {
    padding: 1.1rem 0.95rem;
  }

  .entry-gallery {
    grid-template-columns: 1fr;
  }

  .responsibility-group {
    padding: 0.85rem 0.9rem;
  }

  .responsibility-group li,
  .entry-block li {
    font-size: 0.88rem;
  }
}
</style>
