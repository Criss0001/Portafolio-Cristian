<script setup>
import linkedin from "@/icons/linkedin_icon.svg";
import instagram from "/src/icons/instagram_icon.svg";
import github from "/src/icons/github_icon.svg";
import email from "/src/icons/email_@_icon.svg";
</script>

<template>
  <section class="hero">
    <div class="hero__card">
      <!-- Imagen centrada -->
      <div class="hero__avatar">
        <img src="/src/assets/foto_mia.jpeg" alt="Foto de Cristian Farina" class="avatar__img" />
      </div>

      <!-- Contenido -->
      <div class="hero__content">
        <h1 class="hero__title">Cristian Farina</h1>
        <p class="hero__subtitle">
          Hola, Bienvenido a mi portafolio de proyectos. Soy un desarrollador web con experiencia en
          el desarrollo de aplicaciones web y móviles.
        </p>
        <p class="hero__desc">
          Desarrollo interfaces modernas e interactivas con Vue.js. Apasionado por crear
          experiencias fluidas, optimizadas y con estilos nuevos.
        </p>

        <!-- Redes sociales -->
        <div class="hero__socials">
          <a
            href="https://www.linkedin.com/in/cristian-farina-069aa017b/"
            target="_blank"
            class="social-link linkedin"
            title="LinkedIn"
          >
            <img :src="linkedin" alt="LinkedIn" />
          </a>
          <a
            href="https://github.com/Criss0001"
            target="_blank"
            class="social-link github"
            title="GitHub"
          >
            <img :src="github" alt="GitHub" />
          </a>
          <a
            href="https://instagram.com/cris_farina001"
            target="_blank"
            class="social-link instagram"
            title="Instagram"
          >
            <img :src="instagram" alt="Instagram" />
          </a>
          <a
            href="mailto:cristianjfarina@gmail.com"
            target="_blank" 
            class="social-link email" 
            title="Email"
          >
            <img :src="email" alt="Email" />
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 60px 20px;
}

.hero__card {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.03), rgba(255, 255, 255, 0.01));
  padding: 40px 30px;
  border-radius: 18px;
  box-shadow: 0 6px 20px rgba(2, 6, 23, 0.6);
  max-width: 500px;
  width: 100%;
  transition: transform 0.3s ease;
}
.hero__card:hover {
  transform: translateY(-4px);
}

/* 🔹 Imagen */
.hero__avatar {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 24px;
  box-shadow: 0 10px 25px rgba(2, 6, 23, 0.8);
  border: 2px solid rgba(255, 255, 255, 0.05);
}
.avatar__img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}
.hero__avatar:hover .avatar__img {
  transform: scale(1.08);
}

/* 🔹 Texto */
.hero__title {
  font-size: 28px;
  margin: 0;
}
.hero__subtitle {
  color: var(--muted, #a0a0a0);
  font-size: 15px;
  margin: 6px 0 12px;
}
.hero__desc {
  line-height: 1.6;
  max-width: 400px;
  margin: 0 auto 18px;
  color: var(--text, #eaeaea);
}

/* 🔹 Redes sociales */
.hero__socials {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin: 16px 0 20px;
}
.social-link {
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  transition: all 0.3s ease;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.05);
}
.social-link img {
  width: 22px;
  height: 22px;
  filter: brightness(0.9);
  transition: transform 0.3s ease, filter 0.3s ease;
}

/* Hover de redes */
.social-link:hover {
  transform: scale(1.15);
  box-shadow: 0 0 12px rgba(0, 188, 212, 0.5);
}
.social-link.linkedin:hover {
  background: #0077b5;
}
.social-link.github:hover {
  background: #333;
}
.social-link.instagram:hover {
  background: radial-gradient(
    circle at 30% 107%,
    #fdf497 0%,
    #fdf497 5%,
    #fd5949 45%,
    #d6249f 60%,
    #285aeb 90%
  );
}
.social-link.cv:hover {
  background: #00bcd4;
}

/* 🔹 Botones */
.hero__links {
  display: flex;
  justify-content: center;
  gap: 16px;
}
.hero__links a {
  padding: 10px 16px;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.08);
  transition: all 0.3s ease;
  text-decoration: none;
  color: white;
}
.hero__links a:hover {
  background: var(--accent, #00bcd4);
  color: #021018;
  box-shadow: 0 0 12px rgba(0, 188, 212, 0.5);
}
</style>
