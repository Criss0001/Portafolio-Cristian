<script setup>
const skills = [
  { name: "Vue.js", level: 90 },
  { name: "JavaScript", level: 85 },
  { name: "HTML/CSS", level: 92 },
  { name: "Git", level: 78 },
];
</script>

<template>
  <div class="skills">
    <h2 class="section-title">Habilidades</h2>
    <div class="skills__list">
      <div v-for="(s, idx) in skills" :key="idx" class="skill">
        <div class="skill__head">
          <strong>{{ s.name }}</strong>
          <small>{{ s.level }}%</small>
        </div>
        <div class="skill__bar">
          <div
            class="skill__fill"
            :style="{ width: s.level + '%', transitionDelay: idx * 80 + 'ms' }"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.skill {
  margin-bottom: 12px;
}
.skill__head {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}
.skill__bar {
  height: 10px;
  background: rgba(255, 255, 255, 0.03);
  border-radius: 8px;
  overflow: hidden;
}
.skill__fill {
  height: 100%;
  background: linear-gradient(90deg, var(--accent), var(--accent-2));
  width: 0;
}
/* animate fills on mount */
/* :root { */
/* } */
.skill__fill {
  animation: fill 900ms forwards;
}
@keyframes fill {
  to {
    width: var(--w);
  }
}
</style>
