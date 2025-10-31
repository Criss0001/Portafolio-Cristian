<script setup>
const educacion = [
  {
    fecha: "2024",
    title: "Técnicatura Universitaria en Programación",
    descripcion:
      "Operación y programación de computadoras, desarrollo en distintos lenguajes, análisis y control de sistemas.",
  },
  {
    fecha: "2021",
    title: "Curso Frontend Avanzado",
    descripcion: "HTML5, CSS3, JavaScript moderno y SPA con Vue.js.",
  },
];
</script>

<template>
  <div class="edu">
    <h2 class="section-title">Educación</h2>
    <div class="timeline">
      <div
        v-for="(item, idx) in educacion"
        :key="idx"
        class="timeline__item"
        :style="{ animationDelay: idx * 100 + 'ms' }"
      >
        <div class="timeline__date">{{ item.fecha }}</div>
        <div class="timeline__body">
          <h3>{{ item.title }}</h3>
          <p>{{ item.descripcion }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.section-title {
  font-size: 20px;
  margin-bottom: 14px;
}
.timeline {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.timeline__item {
  display: flex;
  gap: 12px;
  align-items: flex-start;
  padding: 12px;
  border-radius: 12px;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.01), transparent);
  transform: translateY(10px);
  opacity: 0;
  animation: rise 0.45s forwards;
}
.timeline__date {
  min-width: 64px;
  font-weight: 700;
  color: var(--muted);
}
.timeline__body h3 {
  margin: 0;
}
@keyframes rise {
  to {
    transform: none;
    opacity: 1;
  }
}
</style>
