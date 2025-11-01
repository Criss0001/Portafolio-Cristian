<script setup>
import { ref, onMounted } from "vue";

const props = defineProps({ links: Array });
const active = ref(props.links?.[0]?.id || "datos");
const menuAbierto = ref(false);

function goTo(id, e) {
  ripple(e);
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" });
  menuAbierto.value = false; // cierra menú en móvil
}

function scrollTo(id) {
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" });
  menuAbierto.value = false;
}

function ripple(e) {
  const btn = e.currentTarget;
  const circle = document.createElement("span");
  circle.className = "ripple";
  const d = Math.max(btn.clientWidth, btn.clientHeight);
  circle.style.width = circle.style.height = d + "px";
  circle.style.left = e.offsetX - d / 2 + "px";
  circle.style.top = e.offsetY - d / 2 + "px";
  btn.appendChild(circle);
  setTimeout(() => circle.remove(), 500);
}

onMounted(() => {
  const sections = props.links.map((l) => document.getElementById(l.id)).filter(Boolean);
  const obs = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) active.value = entry.target.id;
      });
    },
    { threshold: 0.6 }
  );
  sections.forEach((s) => obs.observe(s));
});
</script>

<template>
  <nav class="nav">
    <div class="nav__container">
      <!-- 🔹 Botón Hamburguesa (solo móvil) -->
      <button class="nav__toggle" @click="menuAbierto = !menuAbierto">
        <span :class="['bar', { active: menuAbierto }]"></span>
        <span :class="['bar', { active: menuAbierto }]"></span>
        <span :class="['bar', { active: menuAbierto }]"></span>
      </button>

      <!-- 🔹 Links -->
      <ul :class="['nav__list', { open: menuAbierto }]">
        <li v-for="link in links" :key="link.id" class="nav__item">
          <button
            :class="['nav__link', { 'is-active': active === link.id }]"
            @click="goTo(link.id, $event)"
          >
            {{ link.label }}
            <span class="nav__underline"></span>
          </button>
        </li>
      </ul>
    </div>
      <button class="nav__cta" @click="scrollTo('proyectos')">Ir a proyectos</button>
  </nav>
</template>

<style scoped>
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 5px 0;
  position: top;
  top: 0;
  background: linear-gradient(180deg, rgba(11, 18, 32, 0.7), rgba(11, 18, 32, 0.4));
  backdrop-filter: blur(6px);
  z-index: 40;
}

.nav__container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 24px;
}

.nav__brand {
  font-weight: 800;
  font-size: 1.4rem;
  color: var(--accent, #00c6ff);
}

/* 🔹 Botón Hamburguesa */
.nav__toggle {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 26px;
  height: 20px;
  background: none;
  border: none;
  cursor: pointer;
}

.bar {
  width: 100%;
  height: 3px;
  background: #fff;
  border-radius: 3px;
  transition: all 0.3s ease;
}

.bar.active:nth-child(1) {
  transform: rotate(45deg) translateY(8px);
}
.bar.active:nth-child(2) {
  opacity: 0;
}
.bar.active:nth-child(3) {
  transform: rotate(-45deg) translateY(-8px);
}

/* 🔹 Lista de navegación */
.nav__list {
  display: flex;
  align-items: center;
  gap: 14px;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav__item {
  position: relative;
}

.nav__link {
  background: transparent;
  border: none;
  padding: 8px 12px;
  border-radius: 8px;
  color: var(--muted, #cbd5e1);
  cursor: pointer;
  position: relative;
  overflow: hidden;
  font-weight: 600;
}

.nav__link:hover {
  color: var(--accent, #00c6ff);
}

.nav__link.is-active {
  color: var(--accent, #00c6ff);
}

.nav__underline {
  position: absolute;
  left: 8px;
  right: 8px;
  height: 3px;
  border-radius: 3px;
  bottom: 6px;
  opacity: 0;
  transform: scaleX(0);
  background: linear-gradient(90deg, var(--accent), var(--accent-2, #0072ff));
  transition: all 0.28s ease;
}

.nav__link.is-active .nav__underline {
  opacity: 1;
  transform: scaleX(1);
}

/* 🔹 Botón CTA */
.nav__cta {
  background: linear-gradient(90deg, var(--accent), var(--accent-2));
  border: 20px;
  padding: 15px 14px;
  border-radius: 12px;
  color: #031926;
  font-weight: 700;
  cursor: pointer;
}

/* 🔹 Modo móvil */
@media (max-width: 768px) {
  .nav__toggle {
    display: flex;
  }

  .nav__list {
    position: absolute;
    top: 64px;
    left: 0;
    width: 100%;
    background: rgba(11, 18, 32, 0.95);
    flex-direction: column;
    align-items: center;
    gap: 16px;
    padding: 20px 0;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.35s ease;
  }

  .nav__list.open {
    max-height: 300px;
  }
}

/* 🔹 Ripple Effect */
.ripple {
  position: absolute;
  border-radius: 50%;
  transform: scale(0);
  animation: r 0.5s linear;
  background: rgba(255, 255, 255, 0.15);
  pointer-events: none;
}

@keyframes r {
  to {
    transform: scale(2);
    opacity: 0;
  }
}
</style>
