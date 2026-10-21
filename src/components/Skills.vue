<template>
  <section id="skills" class="section skills">
    <div class="container">
      <div class="section-head" data-reveal>
        <h2 class="title">Skills</h2>
        <p class="subtitle">Tools I use to clean, analyze, and report data.</p>
        <div class="section-divider"></div>
      </div>

      <div class="skills-listing">
        <article
          v-for="(skill, index) in skills"
          :key="skill.name"
          class="skill-card"
          data-reveal
          :style="{ '--reveal-delay': `${index * 0.06}s` }"
        >
          <div class="skill-card-header">
            <span class="skill-pill">{{ skill.abbrev }}</span>
            <h3>{{ skill.name }}</h3>
          </div>
          <p>{{ skill.details }}</p>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  {
    name: 'Excel',
    abbrev: 'XL',
    details: 'Pivot Tables, VLOOKUP, Data Cleaning & Reporting',
  },
  {
    name: 'Python',
    abbrev: 'Py',
    details: 'Pandas, Matplotlib, Data Analysis',
  },
  {
    name: 'SQL',
    abbrev: 'SQL',
    details: 'Queries, Data Retrieval, Database Management',
  },
  {
    name: 'Power BI',
    abbrev: 'BI',
    details: 'Dashboards, Data Visualization',
  },
]
</script>

<style scoped>
.skills.section {
  padding: 2rem 0 2.5rem;
}

.skills :deep(.section-head) {
  margin-bottom: 1.5rem;
}

.skills :deep(.section-divider) {
  margin-top: 1.1rem;
}

.skills-listing {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 0.9rem;
}

.skill-card {
  padding: 1.15rem 1.1rem;
  background: rgba(18, 28, 51, 0.55);
  border: 1px solid var(--border);
  border-radius: 14px;
  transition: border-color 0.25s ease, background 0.25s ease;
}

.skill-card:hover {
  border-color: var(--border-strong);
  background: rgba(26, 39, 66, 0.65);
}

.skill-card-header {
  display: flex;
  align-items: center;
  gap: 0.7rem;
  margin-bottom: 0.6rem;
}

.skill-pill {
  min-width: 38px;
  height: 38px;
  display: grid;
  place-items: center;
  border-radius: 10px;
  background: rgba(77, 163, 255, 0.12);
  border: 1px solid rgba(77, 163, 255, 0.22);
  color: var(--primary-2);
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.skill-card h3 {
  margin: 0;
  font-size: 1.02rem;
  font-weight: 700;
  color: var(--text);
}

.skill-card p {
  margin: 0;
  line-height: 1.5;
  color: var(--muted);
  font-size: 0.88rem;
}

@media (max-width: 980px) {
  .skills-listing {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 768px) {
  .skills.section {
    padding: 1.75rem 0 2rem;
  }
}

@media (max-width: 520px) {
  .skills.section {
    padding: 1.5rem 0 1.75rem;
  }

  .skills-listing {
    grid-template-columns: 1fr;
    gap: 0.7rem;
  }

  .skill-card {
    padding: 1rem 0.95rem;
  }
}
</style>
