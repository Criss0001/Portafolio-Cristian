<script setup>
import proyecto1 from "/src/assets/PaginaWeb1.png";
import proyecto2 from "/src/assets/Proyecto-Web-Robot.png";
import proyecto3 from "/src/assets/Buscador_peliculas.png";
import proyecto4 from "/src/assets/Calculadora.png";
import proyecto5 from "/src/assets/Clima.png";
import { ref, onMounted } from "vue";

const proyectos = ref([
  {
    titulo: "Pagina Web Experimental I",
    desc: "Creé una pagina web con los distintos estilos que podemos utilizar en CSS para la vista del front end.",
    tools: ["HTML", "CSS"],
    tipo: "Personal",
    img: proyecto1,
    proyectoLink: "https://proyecto-2-css-scode.netlify.app/",
    githubLink: "https://github.com/Criss0001/Proyecto-2-CSS",
  },
  {
    titulo: "Pagina Web Experimental II",
    desc: "Con ésta pagina web comence a ver y aprender a utilizar HTML, estilos de CSS y tambien AI generando imagenes .",
    tools: ["HTML", "CSS", "AI"],
    tipo: "Web",
    img: proyecto2,
    proyectoLink: "",
    githubLink: "https://github.com/Criss0001/Proyecto-curso-HTML/blob/master/favicon.ico",
  },
  {
    titulo: "Buscador de Películas",
    desc: "Construí un buscador de peliculas la cual da información de los títulos que uno le ingresa.",
    tools: ["HTML", "CSS", "JavaScript", "API"],
    tipo: "Proyecto",
    img: proyecto3,
    proyectoLink: "https://proyecto-2-css-scode.netlify.app/",
    githubLink: "https://github.com/Criss0001/Proyecto-2-CSS",
  },
  {
    titulo: "Calculadora",
    desc: "Creé una calculadora básica utilizando JavaScript, HTML y CSS que permite realizar operaciones aritméticas simples.",
    tools: ["JavaScript", "HTML", "CSS", "api"],
    tipo: "Proyecto",
    img: proyecto4,
    proyectoLink: "",
    githubLink: "https://github.com/Criss0001/Proyecto_Calculadora_JS",
  },
  {
    titulo: "Clima",
    desc: "Creé una pagina web básica utilizando JavaScript, HTML y CSS que permite ver el clima en distintos lugares del mundo.",
    tools: ["JavaScript", "HTML", "CSS", "API"],
    tipo: "Proyecto",
    img: proyecto5,
    proyectoLink: "https://aplicacion-clima-java.netlify.app/",
    githubLink: "https://github.com/Criss0001/aplicacion-clima-js",
  },
]);

function handleMove(e, idx) {
  const card = e.currentTarget;
  const rect = card.getBoundingClientRect();
  const x = (e.clientX - rect.left) / rect.width - 0.5;
  const y = (e.clientY - rect.top) / rect.height - 0.5;
  const tiltX = (y * 8).toFixed(2);
  const tiltY = (x * -12).toFixed(2);

  // Aseguramos que el objeto tenga style
  proyectos.value[idx].style = proyectos.value[idx].style || {};
  proyectos.value[
    idx
  ].style.transform = `perspective(800px) rotateX(${tiltX}deg) rotateY(${tiltY}deg) translateY(-6px) scale(1.02)`;
  proyectos.value[idx].style.transition = "transform 120ms ease";
}
function reset(idx) {
  proyectos.value[idx].style = proyectos.value[idx].style || {};
  proyectos.value[idx].style.transform = "none";
  proyectos.value[idx].style.transition = "transform 400ms cubic-bezier(.2,.9,.3,1)";
}

onMounted(() => {
  document
    .querySelectorAll(".project")
    .forEach((el, i) => setTimeout(() => el.classList.add("in"), i * 80));
});
</script>

<template>
  <div class="projects">
    <h2 class="section-titulo">Proyectos</h2>
    <div class="projects__grid">
      <div
        v-for="(p, i) in proyectos"
        :key="i"
        class="project"
        @mousemove="handleMove($event, i)"
        @mouseleave="reset(i)"
      >
        <div class="project__inner" :style="p.style">
          <div class="project__image">
            <img :src="p.img" :alt="p.titulo" />
          </div>

          <div class="project__eyebrow">{{ p.tipo }}</div>
          <h3 class="project__titulo">{{ p.titulo }}</h3>
          <p class="project__desc">{{ p.desc }}</p>
          <div class="project__meta">{{ p.tools.join(" • ") }}</div>

          <!-- Mostrar botones sólo si existe el link -->
          <div class="proyecto-links">
            <a
              v-if="p.proyectoLink"
              :href="p.proyectoLink"
              class="btn-ver-mas"
              target="_blank"
              rel="noopener noreferrer"
            >
              Ver Proyecto
            </a>

            <a
              v-if="p.githubLink"
              :href="p.githubLink"
              class="github-link"
              target="_blank"
              rel="noopener noreferrer"
            >
              Ver Código en GitHub
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* ... tus estilos actuales (ya los tenés) ... */
.projects__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 18px;
}
.project {
  border-radius: 14px;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.01), rgba(255, 255, 255, 0.005));
  padding: 16px;
  cursor: pointer;
  transform: translateY(20px);
  opacity: 0;
  transition: all 0.35s;
}
.project.in {
  transform: none;
  opacity: 1;
}
.project__inner {
  border-radius: 10px;
  padding: 16px;
  height: 100%;
  box-shadow: 0 8px 28px rgba(2, 6, 23, 0.6);
  transition: transform 0.4s ease;
}
.project__image {
  overflow: hidden;
  border-radius: 10px;
  margin-bottom: 10px;
  height: 160px;
}
.project__image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}
.project:hover .project__image img {
  transform: scale(1.05);
}
.project__titulo {
  margin: 10px 0;
}
.project__eyebrow {
  font-size: 12px;
  color: var(--muted);
  font-weight: 700;
}
.project__meta {
  margin-top: 12px;
  color: var(--muted);
  font-size: 13px;
}
.proyecto-links {
  display: flex;
  justify-content: center;
  gap: 16px;
  margin-top: 14px;
}
.proyecto-links a {
  text-decoration: none;
  padding: 10px 18px;
  border-radius: 10px;
  font-weight: 600;
  transition: all 0.3s ease;
}
.btn-ver-mas {
  background: linear-gradient(90deg, #00c6ff, #0072ff);
  color: white;
}
.github-link {
  background: #24292e;
  color: white;
}
.btn-ver-mas:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 10px rgba(0, 114, 255, 0.4);
}
.github-link:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 10px rgba(36, 41, 46, 0.5);
}
</style>
