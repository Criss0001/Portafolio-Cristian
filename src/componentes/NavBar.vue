<script setup>
import { ref, onMounted } from "vue";
const props = defineProps({ links: Array });
const active = ref(props.links?.[0]?.id || "datos");

function goTo(id, e) {
  // click ripple animation
  ripple(e);
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" });
}

function scrollTo(id) {
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" });
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
  // IntersectionObserver to update active link
  const sections = props.links.map((l) => document.getElementById(l.id)).filter(Boolean);
  const obs = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          active.value = entry.target.id;
        }
      });
    },
    { threshold: 0.6 }
  );
  sections.forEach((s) => obs.observe(s));
});
</script>

<template>
  <nav class="nav">

    <ul class="nav__list">
      <li v-for="link in links" :key="link.id" class="nav__item">
        <button
          :class="['nav__link', { 'is-active': active === link.id }]"
          @click="goTo(link.id, $event)"
        >
          {{ link.label }}
          <span class="nav__underline" ></span>
        </button>
      </li>
    </ul>

    <button class="nav__cta" @click="scrollTo('proyectos')">Ir a proyectos</button>
  </nav>
</template>

<style scoped>
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  padding: 14px 0;
  position: top;
  top: 0;
  background: linear-gradient(180deg, rgba(11, 18, 32, 0.7), rgba(11, 18, 32, 0.4));
  backdrop-filter: blur(6px);
  z-index: 40;
}
.nav__brand {
  font-weight: 700;
  letter-spacing: 0.6px;
}
.nav__list {
  display: flex;
  gap: 8px;
  align-items: center;
  list-style: none;
  margin: 0;
  padding: 0;
}
.nav__item {
  position: relative;
}
.nav__link {
  background: transparent;
  border: 0;
  padding: 8px 12px;
  border-radius: 8px;
  color: var(--muted);
  cursor: pointer;
  position: relative;
  overflow: hidden;
  font-weight: 600;
}
.nav__link:hover {
  color: var(--accent);
}
.nav__link.is-active {
  color: var(--accent);
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
  background: linear-gradient(90deg, var(--accent), var(--accent-2));
  transition: all 0.28s ease;
}
.nav__link.is-active .nav__underline {
  opacity: 1;
  transform: scaleX(1);
}

.nav__cta {
  background: linear-gradient(90deg, var(--accent), var(--accent-2));
  border: 0;
  padding: 8px 14px;
  border-radius: 12px;
  color: #031926;
  font-weight: 700;
  cursor: pointer;
}

/* ripple */
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
