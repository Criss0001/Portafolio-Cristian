<script setup>
import { onMounted, ref } from "vue";
const trabajos = [
  {
    role: "Desarrollador Frontend",
    periodo: "2023 - Presente",
    descripcion: "Desarrollo de componentes reutilizables y optimización de rendimiento.",
  },
  {
    role: "Pasante en TI",
    periodo: "2022 - 2023",
    descripcion: "Soporte y mejoras en aplicaciones internas.",
  },
];
const cards = ref([]);
onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((e) => {
        if (e.isIntersecting) e.target.classList.add("in");
      });
    },
    { threshold: 0.2 }
  );
  document.querySelectorAll(".exp__card").forEach((c) => observer.observe(c));
});
</script>

<template>
  <div class="exp">
    <h2 class="section-title">Experiencia</h2>
    <div class="exp__grid">
      <article v-for="(job, i) in trabajos" :key="i" class="exp__card" ref="cards">
        <h3>{{ job.role }}</h3>
        <small class="muted">{{ job.periodo }}</small>
        <p>{{ job.descripcion }}</p>
      </article>
    </div>
  </div>
</template>

<style scoped>
.exp__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}
.exp__card {
  padding: 16px;
  border-radius: 12px;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.02), rgba(255, 255, 255, 0.01));
  transform: translateY(20px);
  opacity: 0;
  transition: all 0.5s cubic-bezier(0.2, 0.9, 0.2, 1);
}
.exp__card.in {
  transform: none;
  opacity: 1;
  box-shadow: 0 10px 30px rgba(2, 6, 23, 0.6);
}
.muted {
  color: var(--muted);
}
</style>
