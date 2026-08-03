<template>
  <section class="section" id="projects">
    <div class="container">
      <h2 class="section-title">Projects</h2>


      <div class="projects-grid featured">
        <article class="card project-card featured-card">
          <div class="project-banner">
            <img src="/image/projects/jomvinhkh.png" alt="JomvinhKH website screenshot" class="project-img">
            <span class="badge">My first Web</span>
          </div>
          <h3 class="card-title">JomvinhKH</h3>
          <p class="project-desc">A static site showcasing places in Cambodia — my first Vue.js project, built with Vite and Tailwind, deployed on Vercel.</p>
          <div class="project-stack mono">
            <span>Vue 3</span><span>Vite</span><span>Tailwind</span>
          </div>
          <div class="project-links">
            <a href="https://jomvinhkh.vercel.app" target="_blank" rel="noopener" class="btn btn-secondary btn-sm">Live Demo</a>
            <a href="https://github.com/yanphayu/JomvinhKH" target="_blank" rel="noopener" class="btn btn-secondary btn-sm">Source</a>
          </div>
        </article>

        <article class="card project-card featured-card">
          <div class="project-banner">
            <img src="/image/projects/rms.png" alt="KitchenFlow — Restaurant Management System screenshot" class="project-img">
            <span class="badge">Full-Stack PHP</span>
          </div>
          <h3 class="card-title">KitchenFlow — Restaurant Management System</h3>
          <p class="project-desc">A restaurant manager built with PHP, MySQL, and jQuery/AJAX — Chart.js dashboard, order/tables/foods/categories management, global search, and role-based login.</p>
          <div class="project-stack mono">
            <span>PHP</span><span>MySQL</span><span>jQuery/AJAX</span><span>Chart.js</span>
          </div>
          <p class="project-login mono"><span class="accent">admin</span> / <span class="accent">1234</span></p>
          <div class="project-links">
            <a href="https://rmszin2.wuaze.com" target="_blank" rel="noopener" class="btn btn-secondary btn-sm">Live Demo</a>
            <a href="https://github.com/yanphayu/Restaurant-Management-System" target="_blank" rel="noopener" class="btn btn-secondary btn-sm">Source</a>
          </div>
        </article>

        <article class="card project-card featured-card">
          <div class="project-banner">
            <img src="/image/projects/yanphayu_v1.png" alt="yanphayu_v1 — my first portfolio website screenshot" class="project-img">
            <span class="badge">Portfolio v1</span>
          </div>
          <h3 class="card-title">yanphayu_v1</h3>
          <p class="project-desc">My very first portfolio website — the earlier iteration of this site, before the redesign.</p>
          <div class="project-stack mono">
            <span>Vue 3</span><span>Vite</span>
          </div>
          <div class="project-links">
            <a href="https://yanphayuv1.vercel.app" target="_blank" rel="noopener" class="btn btn-secondary btn-sm">Live Demo</a>
            <a href="https://github.com/yanphayu/yanphayu_v1" target="_blank" rel="noopener" class="btn btn-secondary btn-sm">Source</a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
