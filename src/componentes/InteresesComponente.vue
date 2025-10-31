<script setup>
const items = [
  { icon: "🎨", title: "Tecnología de Innovación", desc: "Desarrollo de Software de Código Abierto: Contribuyo a proyectos en GitHub, colaborando con otros desarrolladores para mejorar herramientas y librerías populares." },
  { icon: "🧩", title: "Deportes al Aire Libre", desc: "Disfruto de jugar al basketball y futbol actividades que practico regularmente para mantener un equilibrio entre el trabajo y la vida personal." },
  { icon: "🌐", title: "Desarrollo de Software de Código Abierto: ", desc: "Contribuyo a proyectos en GitHub, colaborando con otros desarrolladores para mejorar herramientas y librerías populares." },
];
</script>

<template>
  <div class="interes">
    <h2 class="section-title">Intereses</h2>
    <div class="interes__grid">
      <div v-for="(i, idx) in items" :key="idx" class="interes__item">
        <div class="icon">{{ i.icon }}</div>
        <h4>{{ i.title }}</h4>
        <p>{{ i.desc }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.interes__grid {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}
.interes__item {
  flex: 1 1 220px;
  padding: 16px;
  border-radius: 12px;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.01), transparent);
  transition: transform 0.25s, box-shadow 0.25s;
  cursor: pointer;
}
.interes__item:hover {
  transform: translateY(-6px) scale(1.02);
  box-shadow: 0 12px 30px rgba(2, 6, 23, 0.6);
}
.icon {
  font-size: 28px;
}
</style>
