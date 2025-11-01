<script setup>
import { ref } from "vue";
import NavBar from "./componentes/NavBar.vue";
import DatosPersonales from "./componentes/DatosPersonales.vue";
import EducacionComponente from "./componentes/EducacionComponente.vue";
import ExperienciaComponente from "./componentes/ExperienciaComponente.vue";
import HabilidadesComponente from "./componentes/HabilidadesComponente.vue";
import InteresesComponente from "./componentes/InteresesComponente.vue";
import ProyectoComponente from "./componentes/ProyectoComponente.vue";

const links = ref([
  { id: "datos", label: "Inicio" },
  { id: "educacion", label: "Educación" },
  { id: "experiencia", label: "Experiencia" },
  { id: "habilidades", label: "Habilidades" },
  { id: "intereses", label: "Intereses" },
  { id: "proyectos", label: "Proyectos" },
]);

function scrollToTop() {
  window.scrollTo({
    top: 0,
    behavior: "smooth"
  });
}

</script>

<template>
  <div id="app">
    <NavBar :links="links" />

    <main>
      <section id="datos" class="section section--hero">
        <DatosPersonales />
      </section>

      <section id="educacion" class="section">
        <EducacionComponente />
      </section>

      <section id="experiencia" class="section">
        <ExperienciaComponente />
      </section>

      <section id="habilidades" class="section">
        <HabilidadesComponente />
      </section>

      <section id="intereses" class="section">
        <InteresesComponente />
      </section>

      <section id="proyectos" class="section">
        <ProyectoComponente />
      </section>
    </main>

    <footer>
      <button class="inicio_top" @click="scrollToTop">Inicio</button>
      <p>© 2025 Farina Cristian - Portafolio. Todos los derechos reservados.</p>
    </footer>
  </div>
</template>

<style>
/* Lightweight layout + section spacing */
:root {
  --bg: #172f57;
  --card: #041a46;
  --accent: #7c3aed;
  --accent-2: #06b6d4;
  --muted: #9aa4b2;
}
html,
body,
#app {
  height: 100%;
}
body {
  margin: 0;
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue",
    Arial;
  background: radial-gradient(1000px 400px at 10% 10%, rgba(40, 54, 247, 0.08), transparent),
    var(--bg);
  color: #e6eef6;
}
main {
  max-width: 1100px;
  margin: 40px auto;
  padding: 0 20px;
}
.section {
  padding: 48px 0;
}
.section--hero {
  padding-top: 5px;
}
.footer {
  text-align: center;
  padding: 24px 0;
  color: var(--muted);
}
footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  font-size: 1.3rem;
}
.inicio_top {
  position: center;
  bottom: 24px;
  right: 24px;
  background: linear-gradient(90deg, var(--accent), var(--accent-2));
  color: #fff;
  border: none;
  border-radius: 50px;
  padding: 10px 18px;
  font-weight: 600;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  transition: all 0.5s ease;
}
.inicio_top:hover {
  transform: scale(1.08);
  box-shadow: 0 6px 14px rgba(0,0,0,0.3);
}

</style>
