<script setup>
import { Document, Files, Link, Picture, TrendCharts } from '@element-plus/icons-vue'

const authors = [
  'Zihao Wang',
  'Yuxiang Wei',
  'Xinpeng Zhou',
  'Tianyu Zhang',
  'Tao Liang',
  'Yalong Bai',
  'Hongzhi Zhang',
  'Wangmeng Zuo',
]

const links = [
  { label: 'Paper', href: '/adapref/premier.pdf', icon: Document },
  { label: 'arXiv', href: 'https://arxiv.org/abs/2603.20725', icon: Link },
  { label: 'GitHub', href: 'https://github.com/120L020904/Premier', icon: Files },
]

const highlights = [
  {
    value: 'Learnable',
    label: 'user embedding',
    text: 'Each user preference is represented as a trainable embedding optimized through diffusion loss.',
  },
  {
    value: 'Adaptive',
    label: 'prompt modulation',
    text: 'A preference adapter fuses the user embedding with text tokens and produces token-wise modulation directions.',
  },
  {
    value: 'Cold-start',
    label: 'preference transfer',
    text: 'New users can be represented as linear combinations of learned embeddings when history images are scarce.',
  },
]

const figures = [
  {
    title: 'Qualitative Comparison',
    image: '/adapref/result_compare.png',
    text: 'Premier keeps generated images closer to the visual style implied by user preference histories while preserving the input prompt.',
  },
  {
    title: 'History Length Study',
    image: '/adapref/result_history.png',
    text: 'The learned representation remains stable as preference histories grow and supports direct training or linear-combination adaptation.',
  },
  {
    title: 'Ablation',
    image: '/adapref/result_abla.png',
    text: 'Ablation results show how the adapter design and preference training choices contribute to user-aligned generation.',
  },
]

const bibtex = `@article{wang2026premier,
  title={Premier: Personalized Preference Modulation with Learnable User Embedding in Text-to-Image Generation},
  author={Wang, Zihao and Wei, Yuxiang and Zhou, Xinpeng and Zhang, Tianyu and Liang, Tao and Bai, Yalong and Zhang, Hongzhi and Zuo, Wangmeng},
  journal={arXiv preprint arXiv:2603.20725},
  year={2026}
}`
</script>

<template>
  <main class="page-shell">
    <nav class="topbar" aria-label="Primary">
      <a class="brand" href="#">
        <img src="/adapref/project-icon.png" alt="" />
        <span>Premier</span>
      </a>
      <div class="nav-links">
        <a href="#method">Method</a>
        <a href="#results">Results</a>
        <a href="https://github.com/120L020904/Premier" target="_blank" rel="noreferrer">GitHub</a>
        <a href="#bibtex">BibTeX</a>
      </div>
    </nav>

    <section class="hero">
      <div class="hero-copy">
        <div class="paper-badges">
          <span>CVPR 2026</span>
          <span>Highlight</span>
        </div>
        <img class="project-icon" src="/adapref/project-icon.png" alt="Premier project icon" />
        <h1>Premier: Personalized Preference Modulation with Learnable User Embedding in Text-to-Image Generation</h1>
        <p class="subtitle">
          Learn compact user preference embeddings from preference images, then inject them into text-to-image generation through token-wise modulation.
        </p>
        <div class="authors" aria-label="Authors">
          <span v-for="author in authors" :key="author">{{ author }}</span>
        </div>
        <p class="affiliations">Harbin Institute of Technology / Duxiaoman</p>
        <div class="actions">
          <a v-for="item in links" :key="item.label" class="action" :href="item.href" target="_blank" rel="noreferrer">
            <el-icon><component :is="item.icon" /></el-icon>
            <span>{{ item.label }}</span>
          </a>
        </div>
      </div>
      <figure class="hero-media">
        <img src="/adapref/teaser.png" alt="Premier comparison teaser showing user preference images and generated results from several methods." />
        <figcaption>
          User preference images alone guide Premier toward personalized outputs without requiring preference descriptions.
        </figcaption>
      </figure>
    </section>

    <section class="abstract-section">
      <h2>Abstract</h2>
      <p>
        Text-to-image generation has advanced rapidly, yet it still struggles to capture nuanced user preferences. Premier represents each user's preference as a learnable embedding and introduces a preference adapter that fuses the user embedding with the text prompt. The fused preference embedding modulates the generative process, while a dispersion loss encourages distinct user-specific directions. For new users with limited histories, Premier estimates robust preference embeddings as linear combinations of training-set user embeddings.
      </p>
    </section>

    <section class="highlights" aria-label="Method highlights">
      <article v-for="item in highlights" :key="item.value">
        <strong>{{ item.value }}</strong>
        <span>{{ item.label }}</span>
        <p>{{ item.text }}</p>
      </article>
    </section>

    <section id="method" class="figure-section method-section">
      <div class="section-heading">
        <el-icon><Picture /></el-icon>
        <h2>Method</h2>
      </div>
      <p>
        The real method figure shows the preference adapter training framework, adapter module, and new-user embedding training path. User tokens and prompt tokens jointly produce modulation directions for MM-DiT blocks.
      </p>
      <figure class="wide-figure">
        <img src="/adapref/fig_method.png" alt="Premier method diagram with preference adapter training, adapter module, and new user embedding training." />
      </figure>
    </section>

    <section id="results" class="results-section">
      <div class="section-heading">
        <el-icon><TrendCharts /></el-icon>
        <h2>Results</h2>
      </div>
      <div class="result-list">
        <article v-for="figure in figures" :key="figure.title" class="result-item">
          <div class="result-copy">
            <h3>{{ figure.title }}</h3>
            <p>{{ figure.text }}</p>
          </div>
          <img :src="figure.image" :alt="figure.title" />
        </article>
      </div>
    </section>

    <section id="bibtex" class="bibtex-section">
      <h2>BibTeX</h2>
      <pre><code>{{ bibtex }}</code></pre>
    </section>
  </main>
</template>

<style>
:root {
  color: #1b1f23;
  background: #fbfaf7;
  font-family: Inter, "DingTalk Sans", "Segoe UI", Arial, sans-serif;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.85), rgba(251, 250, 247, 0.96)),
    #fbfaf7;
}

a {
  color: inherit;
  text-decoration: none;
}

img {
  display: block;
  max-width: 100%;
}

.page-shell {
  min-height: 100vh;
}

.topbar {
  position: sticky;
  top: 0;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  min-height: 58px;
  padding: 0 5vw;
  border-bottom: 1px solid rgba(27, 31, 35, 0.08);
  background: rgba(251, 250, 247, 0.92);
  backdrop-filter: blur(16px);
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-weight: 800;
  font-size: 20px;
  color: #134e4a;
}

.brand img {
  width: 30px;
  height: 30px;
  border-radius: 7px;
  object-fit: cover;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 22px;
  color: #4b5563;
  font-size: 14px;
  font-weight: 650;
}

.nav-links a:hover {
  color: #c2410c;
}

.hero {
  display: grid;
  grid-template-columns: minmax(320px, 0.78fr) minmax(480px, 1.22fr);
  gap: 44px;
  align-items: center;
  max-width: 1440px;
  margin: 0 auto;
  padding: 54px 5vw 36px;
}

.paper-badges {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 18px;
}

.paper-badges span {
  display: inline-flex;
  align-items: center;
  min-height: 30px;
  padding: 0 11px;
  border: 1px solid rgba(194, 65, 12, 0.18);
  border-radius: 999px;
  background: #fff7ed;
  color: #c2410c;
  font-size: 13px;
  font-weight: 850;
  letter-spacing: 0;
  text-transform: uppercase;
}

.paper-badges span:nth-child(2) {
  border-color: rgba(15, 118, 110, 0.2);
  background: #ecfdf5;
  color: #0f766e;
}

.project-icon {
  width: 86px;
  height: 86px;
  margin-bottom: 20px;
  border: 1px solid rgba(27, 31, 35, 0.08);
  border-radius: 20px;
  object-fit: cover;
  box-shadow: 0 14px 28px rgba(15, 23, 42, 0.08);
}

h1,
h2,
h3,
p {
  margin-top: 0;
}

h1 {
  max-width: 820px;
  margin-bottom: 18px;
  color: #111827;
  font-size: 48px;
  line-height: 1.05;
  letter-spacing: 0;
}

h2 {
  margin-bottom: 18px;
  color: #111827;
  font-size: 30px;
  line-height: 1.15;
  letter-spacing: 0;
}

h3 {
  margin-bottom: 12px;
  color: #111827;
  font-size: 22px;
  line-height: 1.2;
  letter-spacing: 0;
}

.subtitle {
  max-width: 760px;
  margin-bottom: 22px;
  color: #334155;
  font-size: 19px;
  line-height: 1.55;
}

.authors {
  display: flex;
  flex-wrap: wrap;
  gap: 8px 16px;
  max-width: 760px;
  color: #0f766e;
  font-weight: 700;
  line-height: 1.45;
}

.affiliations {
  margin: 14px 0 24px;
  color: #64748b;
  font-size: 15px;
}

.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.action {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  min-height: 42px;
  padding: 0 16px;
  border: 1px solid #0f766e;
  border-radius: 6px;
  background: #0f766e;
  color: #ffffff;
  font-weight: 750;
}

.action:nth-child(n + 2) {
  border-color: rgba(15, 118, 110, 0.25);
  background: #ffffff;
  color: #0f766e;
}

.action:hover {
  transform: translateY(-1px);
  box-shadow: 0 10px 24px rgba(15, 118, 110, 0.16);
}

.hero-media {
  margin: 0;
}

.hero-media img,
.wide-figure,
.result-item img {
  border: 1px solid rgba(27, 31, 35, 0.08);
  border-radius: 8px;
  background: #ffffff;
  box-shadow: 0 18px 40px rgba(15, 23, 42, 0.08);
}

figcaption {
  margin-top: 12px;
  color: #64748b;
  font-size: 14px;
  line-height: 1.45;
}

.abstract-section,
.figure-section,
.results-section,
.bibtex-section {
  max-width: 1240px;
  margin: 0 auto;
  padding: 54px 5vw;
}

.abstract-section p,
.figure-section > p {
  max-width: 980px;
  color: #334155;
  font-size: 18px;
  line-height: 1.7;
}

.highlights {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
  max-width: 1240px;
  margin: 0 auto;
  padding: 0 5vw 46px;
}

.highlights article {
  min-height: 170px;
  padding: 24px;
  border: 1px solid rgba(27, 31, 35, 0.08);
  border-radius: 8px;
  background: #ffffff;
}

.highlights strong {
  display: block;
  color: #c2410c;
  font-size: 28px;
  line-height: 1.1;
}

.highlights span {
  display: block;
  margin: 6px 0 14px;
  color: #111827;
  font-weight: 800;
}

.highlights p,
.result-copy p {
  margin-bottom: 0;
  color: #475569;
  line-height: 1.6;
}

.section-heading {
  display: flex;
  align-items: center;
  gap: 10px;
}

.section-heading .el-icon {
  color: #0f766e;
  font-size: 27px;
}

.wide-figure {
  margin: 28px 0 0;
  padding: 18px;
}

.wide-figure img {
  margin: 0 auto;
}

.results-section {
  background: #f2f7f5;
  max-width: none;
}

.results-section > .section-heading,
.result-list {
  max-width: 1240px;
  margin-right: auto;
  margin-left: auto;
}

.result-list {
  display: grid;
  gap: 26px;
}

.result-item {
  display: grid;
  grid-template-columns: 260px minmax(0, 1fr);
  gap: 26px;
  align-items: start;
}

.result-copy {
  position: sticky;
  top: 82px;
  padding-top: 8px;
}

.result-item img {
  width: 100%;
  padding: 12px;
}

.bibtex-section pre {
  overflow-x: auto;
  margin: 0;
  padding: 20px;
  border: 1px solid rgba(27, 31, 35, 0.08);
  border-radius: 8px;
  background: #111827;
  color: #f8fafc;
  font-size: 15px;
  line-height: 1.55;
}

@media (max-width: 980px) {
  .hero,
  .result-item {
    grid-template-columns: 1fr;
  }

  h1 {
    font-size: 38px;
  }

  .highlights {
    grid-template-columns: 1fr;
  }

  .result-copy {
    position: static;
  }
}

@media (max-width: 640px) {
  .topbar {
    align-items: flex-start;
    flex-direction: column;
    gap: 8px;
    padding-top: 12px;
    padding-bottom: 12px;
  }

  .nav-links {
    width: 100%;
    justify-content: space-between;
    gap: 10px;
  }

  .hero {
    padding-top: 34px;
  }

  h1 {
    font-size: 31px;
  }

  h2 {
    font-size: 25px;
  }

  .subtitle,
  .abstract-section p,
  .figure-section > p {
    font-size: 16px;
  }

  .wide-figure,
  .result-item img {
    padding: 8px;
  }
}
</style>
