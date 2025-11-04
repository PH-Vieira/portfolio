<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { ScrollToPlugin } from 'gsap/ScrollToPlugin';

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin);

const navLinks = [
  { label: 'Sobre', target: '#about' },
  { label: 'Interesses', target: '#interests' },
  { label: 'Projetos', target: '#projects' },
  { label: 'Skills', target: '#skills' },
  { label: 'Experiência', target: '#experience' },
  { label: 'Contato', target: '#contact' },
];

const profile = {
  name: 'Pedro Henrique Vieira',
  availabilityNote: 'disponível para projetos full-stack',
  hero: {
    title: 'Desenvolvedor Full-Stack',
    subtitle:
      'Especialista em desenvolvimento web full-stack, com domínio em Vue.js 3, Tailwind CSS e Node.js. Apaixonado por algoritmos avançados como Dijkstra e Modelo Oculto de Markov, trabalho com Linux e busco constantemente inovar na área de TI.',
    ctas: [
      { label: 'Ver projetos', target: '#projects', variant: 'primary' },
      { label: 'Sobre mim', target: '#about', variant: 'secondary' },
    ],
    metrics: [
      { label: 'Anos de experiência', value: '4+' },
      { label: 'Incidentes resolvidos no NOC', value: '200+' },
      { label: 'Dashboards criados', value: '15+' },
      { label: 'Projetos pessoais', value: '5+' },
    ],
    stackHighlights: [
      { label: 'Vue.js + Vite', tag: 'frontend' },
      { label: 'Node.js + Python', tag: 'backend' },
      { label: 'Tailwind CSS', tag: 'estilo' },
      { label: 'Linux', tag: 'ambiente' },
    ],
    availabilityMessage: 'Disponível para projetos full-stack remotos, mentorias e colaborações em defesa aeroespacial.',
  },
  values: [
    'Inovação constante através de algoritmos e tecnologias emergentes.',
    'Excelência técnica aliada à eficiência prática.',
    'Aprendizado contínuo e compartilhamento de conhecimento.',
  ],
  industries:
    'Aeroespacial, defesa, commodities e energia.',
  contact: [
    { label: 'Email', value: 'p0h2@yahoo.com', href: 'mailto:p0h2@yahoo.com' },
    { label: 'WhatsApp', value: '(16) 9 9993-4112', href: 'wa.me/16999934112' },
    { label: 'LinkedIn', value: 'Pedro Henrique Vieira', href: 'https://www.linkedin.com/in/pedro-henrique-vieira-2426a31b7/' },
    { label: 'GitHub', value: '/PH-Vieira', href: 'https://github.com/PH-Vieira' },
  ],
  socials: [
    { label: 'GitHub', href: 'https://github.com/PH-Vieira' },
    { label: 'LinkedIn', href: 'https://www.linkedin.com/in/pedro-henrique-vieira-2426a31b7/' },
    { label: 'Instagram', href: '#' },
  ],
  newsletterText: 'Fatos aleatórios pouco conhecidos sobre tecnologia, defesa e inovação.',
};

const projects = [
  {
    title: 'Planner de Aulas para Professores',
    description:
      'Plataforma interativa e intuitiva para planejamento educacional, otimizando o tempo dos professores com ferramentas avançadas de organização e acompanhamento de aulas.',
    stack: ['React.js', 'Node.js', 'PostgreSQL'],
    link: 'https://aula-planner-charm.lovable.app/',
  },
  {
    title: 'Creators Hub',
    description:
      'Comunidade online para criadores de conteúdo, oferecendo recursos de colaboração, networking e crescimento profissional em um ambiente dinâmico e inspirador.',
    stack: ['Vue.js', 'Supabase', 'Tailwind CSS'],
    link: 'https://creators-hub-xi.vercel.app/',
  },
  {
    title: 'Sistema ERP em Construção',
    description:
      'Solução completa de gestão empresarial, integrando módulos de vendas, estoque e finanças para otimizar operações e tomada de decisões estratégicas.',
    stack: ['Vue.js', 'Node.js', 'PostgreSQL'],
    link: 'https://creators-hub-xi.vercel.app/',
  },
];

const skillGroups = [
  {
    title: 'Frontend',
    items: ['HTML5 - CSS3 - JavaScript', 'Vue.js - Vite - Tailwind CSS'],
  },
  {
    title: 'Backend',
    items: ['Node.js - C - Python', 'PHP (experiência anterior)'],
  },
  {
    title: 'Outros',
    items: ['Linux', 'Metodologias Ágeis', 'Algoritmos Avançados'],
  },
];

const timeline = [
  {
    role: 'Analista NOC',
    company: 'SONDA • Embraer',
    period: 'mai/2025 - Atual',
    description:
      'Monitoramento 24/7 da infraestrutura crítica da Embraer, respondendo a incidentes e coordenando ações corretivas junto às equipes internas.',
  },
  {
    role: 'Mecânico Eletricista',
    company: 'Embraer',
    period: 'mai/2024 - abr/2025',
    description:
      'Montagem e testes em aeronaves executivas e militares, garantindo qualidade e conformidade em sistemas elétricos.',
  },
  {
    role: 'Trainee Desenvolvedor Full-Stack',
    company: 'Embraer',
    period: 'mai/2022 - abr/2024',
    description:
      'Desenvolvimento de aplicações web full-stack usando Vue.js e Node.js. Otimização de apps existentes, documentação e melhoria de algoritmos.',
  },
  {
    role: 'Trainee Suporte de TI',
    company: 'GasBrasiliano (Necta)',
    period: 'dez/2021 - abr/2022',
    description:
      'Manutenção de computadores, atualização de software e instalação de sistemas operacionais.',
  },
  {
    role: 'Aprendiz',
    company: 'Louis Dreyfus Company',
    period: 'jul/2021 - nov/2021',
    description:
      'Pesagem de caminhos e gerenciamento da entrada e saída de matéria-prima e produtos.',
  },
];

const animationVariants = {
  'fade-up': {
    from: { opacity: 0, y: 60 },
    to: { y: 0 },
  },
  'fade-right': {
    from: { opacity: 0, x: -60 },
    to: { x: 0 },
  },
  'blur-in': {
    from: { opacity: 0, filter: 'blur(16px)', y: 24 },
    to: { filter: 'blur(0px)', y: 0, duration: 1.1 },
  },
  'tilt-in': {
    from: { opacity: 0, rotateX: 16, y: 70, transformOrigin: 'top center' },
    to: { rotateX: 0, y: 0 },
  },
  'clip-in': {
    from: { opacity: 0, clipPath: 'inset(0 0 100% 0)' },
    to: { clipPath: 'inset(0 0 0 0)', duration: 1.2, ease: 'power3.out' },
  },
  'scale-pop': {
    from: { opacity: 0, scale: 0.85, y: 30 },
    to: { scale: 1, y: 0 },
  },
  'drift-in': {
    from: { opacity: 0, x: 45, y: 40, rotateZ: 6 },
    to: { x: 0, y: 0, rotateZ: 0 },
  },
  'card-flight': {
    from: { opacity: 0, y: 90, rotateY: -14, transformPerspective: 900 },
    to: { y: 0, rotateY: 0 },
  },
};

const appRoot = ref(null);
const currentYear = new Date().getFullYear();

const scrollToTarget = (target) => {
  gsap.to(window, {
    duration: 0.8,
    scrollTo: target,
    ease: 'power2.out',
  });
};

let ctx;

onMounted(() => {
  ctx = gsap.context(() => {
    const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

    const animateElement = (element, index = 0) => {
      const variantKey = element.dataset.animate || 'fade-up';
      const variant = animationVariants[variantKey] || animationVariants['fade-up'];
      const customDelay = element.dataset.animateDelay ? parseFloat(element.dataset.animateDelay) : null;
      const baseDelay = customDelay ?? Math.min(index * 0.08, 0.4);
      const start = element.dataset.animateStart || 'top 80%';
      const toggleActions = element.dataset.animateToggle || 'play none none reverse';
      const once = element.dataset.animateOnce === 'true';
      const end = element.dataset.animateEnd;
      const scrubValue = element.dataset.animateScrub;
      const markers = element.dataset.animateMarkers === 'true';

      const appliedFrom = prefersReducedMotion ? { opacity: 0 } : { ...variant.from };
      const appliedTo = prefersReducedMotion ? { opacity: 1, y: 0, x: 0, scale: 1 } : { ...variant.to };

      const duration = variant.duration ?? (prefersReducedMotion ? 0.45 : 0.95);
      const ease = variant.ease ?? (prefersReducedMotion ? 'power1.out' : 'power3.out');

      if (!('opacity' in appliedFrom)) {
        appliedFrom.opacity = 0;
      }
      if (!('opacity' in appliedTo)) {
        appliedTo.opacity = 1;
      }

      const triggerTarget = element.dataset.animateTrigger
        ? document.querySelector(element.dataset.animateTrigger)
        : element;

      const scrollTriggerConfig = {
        trigger: triggerTarget || element,
        start,
        once,
      };

      if (scrubValue !== undefined) {
        scrollTriggerConfig.scrub = scrubValue === '' || scrubValue === 'true' ? true : Number(scrubValue);
      } else {
        scrollTriggerConfig.toggleActions = toggleActions;
      }

      if (end) {
        scrollTriggerConfig.end = end;
      }

      if (markers) {
        scrollTriggerConfig.markers = true;
      }

      if (!prefersReducedMotion) {
        gsap.set(element, { willChange: 'transform, opacity' });
        scrollTriggerConfig.onLeave = () => element.style.removeProperty('will-change');
        scrollTriggerConfig.onLeaveBack = () => gsap.set(element, { willChange: 'transform, opacity' });
        scrollTriggerConfig.onEnter = () => gsap.set(element, { willChange: 'transform, opacity' });
      }

      gsap.fromTo(element, appliedFrom, {
        duration,
        ease,
        delay: prefersReducedMotion ? 0 : baseDelay,
        ...appliedTo,
        scrollTrigger: scrollTriggerConfig,
      });
    };

    const registerAnimations = (container) => {
      if (!container) return;
      const elements = gsap.utils.toArray('[data-animate]', container);
      elements.forEach((element, index) => animateElement(element, index));
    };

    if (!prefersReducedMotion) {
      const heroTimeline = gsap.timeline({ defaults: { ease: 'power3.out', duration: 1 } });
      heroTimeline
        .from('.js-hero-badge', { y: -20, opacity: 0, rotateX: 35 })
        .from('.js-hero-title', { clipPath: 'inset(0 0 100% 0)', duration: 1.1, ease: 'power4.out' }, '-=0.7')
        .from('.js-hero-subtitle', { y: 28, opacity: 0, filter: 'blur(18px)' }, '-=0.6')
        .from('.js-hero-actions', { y: 24, opacity: 0, rotationX: 12, stagger: 0.12 }, '-=0.5')
        .from('.js-hero-stats > div', { opacity: 0, y: 32, stagger: 0.08 }, '-=0.6');

      gsap.to('.js-hero-card', {
        y: -40,
        rotateX: 8,
        ease: 'none',
        scrollTrigger: {
          trigger: '#hero',
          start: 'top top',
          end: 'bottom top',
          scrub: true,
        },
      });
    }

    registerAnimations(document.querySelector('.js-hero'));
    gsap.utils.toArray('.js-section').forEach((section) => registerAnimations(section));

    if (!prefersReducedMotion) {
      gsap.utils.toArray('[data-parallax]').forEach((layer) => {
        const amplitude = Number(layer.dataset.parallax) || 20;
        const targetSelector = layer.dataset.parallaxTarget;
        const trigger = targetSelector ? document.querySelector(targetSelector) : layer;

        gsap.to(layer, {
          yPercent: amplitude,
          ease: 'none',
          scrollTrigger: {
            trigger: trigger || layer,
            start: 'top bottom',
            end: 'bottom top',
            scrub: true,
          },
        });
      });
    }
  }, appRoot.value);
});

onBeforeUnmount(() => {
  ctx?.revert();
  ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
});
</script>

<template>
  <div ref="appRoot" class="relative min-h-screen overflow-hidden bg-gradient-to-b from-halloween-black via-black to-neutral-950 text-white">
    <span
      aria-hidden="true"
      class="pointer-events-none absolute -left-32 top-24 h-80 w-80 rounded-full bg-halloween-purple/35 blur-3xl mix-blend-screen"
      data-parallax="-18"
      data-parallax-target="#hero"
    ></span>
    <span
      aria-hidden="true"
      class="pointer-events-none absolute right-[-18%] top-1/2 h-[28rem] w-[28rem] translate-y-[-50%] rounded-full bg-halloween-orange/25 blur-3xl mix-blend-screen"
      data-parallax="24"
      data-parallax-target="#projects"
    ></span>
    <!-- Decorative elements on the sides -->
    <span
      aria-hidden="true"
      class="pointer-events-none absolute left-8 top-1/3 h-16 w-16 rounded-full bg-halloween-green/20 blur-xl"
      data-parallax="-5"
      data-animate="fade-up"
      data-animate-delay="0.5"
    ></span>
    <span
      aria-hidden="true"
      class="pointer-events-none absolute left-16 bottom-1/3 h-24 w-24 rounded-lg bg-halloween-purple/15 blur-2xl rotate-45"
      data-parallax="8"
      data-animate="scale-pop"
      data-animate-delay="0.7"
    ></span>
    <span
      aria-hidden="true"
      class="pointer-events-none absolute right-8 top-2/3 h-20 w-20 rounded-full bg-halloween-orange/25 blur-2xl"
      data-parallax="12"
      data-animate="fade-up"
      data-animate-delay="0.6"
    ></span>
    <span
      aria-hidden="true"
      class="pointer-events-none absolute right-12 bottom-1/4 h-32 w-32 rounded-full bg-halloween-purple/10 blur-3xl"
      data-parallax="-15"
      data-animate="drift-in"
      data-animate-delay="0.8"
    ></span>
    <header class="fixed top-0 left-0 right-0 z-50 border-b border-white/10 bg-black/70 backdrop-blur">
      <nav class="mx-auto flex max-w-6xl items-center justify-between px-6 py-4">
        <div class="flex items-center gap-3">
          <span class="js-hero-badge inline-flex items-center gap-2 rounded-full border border-white/10 bg-white/5 px-3 py-1 text-xs uppercase tracking-[0.2em] text-halloween-orange">
            <span class="h-2 w-2 rounded-full bg-halloween-orange"></span>
            {{ profile.availabilityNote }}
          </span>
        </div>
        <ul class="hidden items-center gap-6 text-sm font-medium md:flex">
          <li v-for="link in navLinks" :key="link.target">
            <a
              :href="link.target"
              class="text-white/80 transition hover:text-halloween-orange"
              @click.prevent="scrollToTarget(link.target)"
            >
              {{ link.label }}
            </a>
          </li>
        </ul>
        <button
          class="rounded-full border border-white/10 bg-halloween-purple px-4 py-2 text-sm font-semibold text-white shadow-lg shadow-halloween-purple/40 transition hover:-translate-y-0.5 hover:shadow-xl"
          @click.prevent="scrollToTarget('#contact')"
        >
          Vamos conversar
        </button>
      </nav>
    </header>

    <main class="mx-auto max-w-6xl px-6 pt-24">
      <section id="hero" class="js-hero pt-16 pb-32">
        <div class="grid gap-16 lg:grid-cols-[minmax(0,1fr)_360px]">
          <div class="space-y-6">
            <h1 class="js-hero-title text-4xl font-bold text-white md:text-5xl lg:text-6xl">
              {{ profile.hero.title }}
            </h1>
            <p class="js-hero-subtitle max-w-2xl text-lg text-white/70">
              {{ profile.hero.subtitle }}
            </p>
            <div class="js-hero-actions flex flex-wrap gap-4">
              <button
                v-for="cta in profile.hero.ctas"
                :key="cta.label"
                type="button"
                :class="[
                  'rounded-full px-6 py-3 font-semibold transition',
                  cta.variant === 'primary'
                    ? 'bg-halloween-orange text-black shadow-lg shadow-halloween-orange/40 hover:-translate-y-0.5'
                    : 'border border-white/15 text-white/80 hover:border-white/40 hover:text-white'
                ]"
                @click="scrollToTarget(cta.target)"
              >
                {{ cta.label }}
              </button>
              <a
                href="/cv.pdf"
                download
                class="rounded-full border border-white/15 px-6 py-3 font-semibold text-white/80 transition hover:border-white/40 hover:text-white"
              >
                Baixar CV
              </a>
            </div>
            <dl class="js-hero-actions js-hero-stats grid grid-cols-2 gap-8 text-sm uppercase tracking-wide text-white/50 md:grid-cols-4">
              <div v-for="metric in profile.hero.metrics" :key="metric.label">
                <dt class="text-white/40">{{ metric.label }}</dt>
                <dd class="text-3xl font-bold text-white">{{ metric.value }}</dd>
              </div>
            </dl>
          </div>

          <div class="relative flex items-center justify-center">
            <div
              class="js-hero-card h-full w-full max-w-sm rounded-3xl border border-white/10 bg-gradient-to-br from-white/5 via-white/10 to-white/5 p-8 backdrop-blur"
              data-animate="card-flight"
              data-animate-start="top 92%"
              data-animate-once="true"
            >
              <p class="text-sm uppercase tracking-[0.4em] text-white/50">Stack atual</p>
              <ul class="mt-6 space-y-4 text-base text-white/80">
                <li
                  v-for="(item, index) in profile.hero.stackHighlights"
                  :key="item.label"
                  class="flex items-center justify-between"
                  :class="index < profile.hero.stackHighlights.length - 1 ? 'border-b border-white/10 pb-3' : ''"
                >
                  <span>{{ item.label }}</span>
                  <span class="text-xs text-white/50">{{ item.tag }}</span>
                </li>
              </ul>
              <div class="mt-8 rounded-2xl border border-white/10 bg-black/60 p-4">
                <p class="text-sm text-white/60">{{ profile.hero.availabilityMessage }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section id="about" class="js-section border-t border-white/10 py-24">
        <div class="grid gap-12 lg:grid-cols-[minmax(0,1fr)_320px]">
          <div class="space-y-6">
            <h2
              class="text-3xl font-semibold text-white md:text-4xl"
              data-animate="blur-in"
              data-animate-scrub="0.8"
              data-animate-end="+=200"
            >
              Sobre Mim: Paixão por Tecnologia e Inovação
            </h2>
            <p
              class="text-lg text-white/70"
              data-animate="blur-in"
              data-animate-scrub="0.7"
              data-animate-end="+=200"
            >
              Especialista em desenvolvimento web full-stack, combino expertise em front-end com Vue.js 3 e Tailwind CSS, e back-end robusto com Node.js, criando soluções eficientes e escaláveis.
            </p>
            <p
              class="text-lg text-white/70"
              data-animate="fade-up"
              data-animate-delay="0.12"
              data-animate-scrub="0.75"
              data-animate-end="+=220"
            >
              Profundo conhecedor de algoritmos e estruturas de dados, aplico técnicas como pesquisa em largura, Dijkstra e Modelo Oculto de Markov em projetos reais. Trabalhando com confiança em Linux, estou sempre explorando novas tecnologias para impulsionar a inovação em TI.
            </p>
          </div>
          <div class="space-y-6">
            <div
              class="rounded-3xl border border-white/10 bg-white/5 p-8"
              data-animate="tilt-in"
              data-animate-scrub="0.9"
              data-animate-end="bottom 55%"
            >
              <h3 class="text-sm uppercase tracking-[0.3em] text-white/50">Valores</h3>
              <ul class="mt-4 space-y-4 text-base text-white/70">
                <li v-for="value in profile.values" :key="value">• {{ value }}</li>
              </ul>
            </div>
            <div
              class="rounded-3xl border border-white/10 bg-black/60 p-8"
              data-animate="drift-in"
              data-animate-delay="0.1"
              data-animate-scrub="1"
              data-animate-end="bottom 45%"
            >
              <h3 class="text-sm uppercase tracking-[0.3em] text-white/50">Trabalho com</h3>
              <p class="mt-3 text-white/70">{{ profile.industries }}</p>
            </div>
          </div>
        </div>
      </section>

      <section id="interests" class="js-section border-t border-white/10 py-24">
        <header class="mb-12 space-y-4">
          <h2
            class="text-3xl font-semibold text-white md:text-4xl"
            data-animate="blur-in"
            data-animate-scrub="0.8"
            data-animate-end="+=200"
          >
            Interesses & Curiosidades
          </h2>
          <p
            class="max-w-2xl text-lg text-white/70"
            data-animate="blur-in"
            data-animate-scrub="1"
            data-animate-end="+=250"
          >
            Além do código, exploro áreas que expandem minha visão técnica e criativa, aplicando conhecimentos matemáticos e computacionais em contextos diversos.
          </p>
        </header>
        <div class="grid gap-8 md:grid-cols-2">
          <div
            class="rounded-3xl border border-white/10 bg-white/5 p-8"
            data-animate="tilt-in"
            data-animate-scrub="0.9"
            data-animate-end="bottom 55%"
          >
            <h3 class="text-xl font-semibold text-white mb-4">Cálculo Numérico & Estatística</h3>
            <p class="text-white/70">
              Apaixonado por resolver problemas complexos com métodos numéricos e análise estatística, aplicando em projetos de otimização e predição.
            </p>
          </div>
          <div
            class="rounded-3xl border border-white/10 bg-black/60 p-8"
            data-animate="drift-in"
            data-animate-delay="0.1"
            data-animate-scrub="1"
            data-animate-end="bottom 45%"
          >
            <h3 class="text-xl font-semibold text-white mb-4">Modelo Oculto de Markov</h3>
            <p class="text-white/70">
              Estudo e implementação de HMMs para modelagem de sequências probabilísticas, útil em reconhecimento de padrões e previsões.
            </p>
          </div>
          <div
            class="rounded-3xl border border-white/10 bg-white/5 p-8"
            data-animate="scale-pop"
            data-animate-delay="0.2"
            data-animate-scrub="0.8"
            data-animate-end="bottom 50%"
          >
            <h3 class="text-xl font-semibold text-white mb-4">Análise de Sinais com Programação</h3>
            <p class="text-white/70">
              Implementação de algoritmos de processamento de sinais digitais, como FFT e filtros, para aplicações em engenharia e dados.
            </p>
          </div>
        </div>
      </section>

      <section id="projects" class="js-section border-t border-white/10 py-24">
        <header class="mb-12 space-y-4">
          <h2
            class="text-3xl font-semibold text-white md:text-4xl"
            data-animate="blur-in"
            data-animate-scrub="0.8"
            data-animate-end="+=200"
          >
            Projetos em destaque
          </h2>
          <p
            class="max-w-2xl text-lg text-white/70"
            data-animate="blur-in"
            data-animate-scrub="1"
            data-animate-end="+=250"
          >
            Seleção de projetos que demonstram expertise em desenvolvimento full-stack, resolução de problemas complexos e entrega de soluções impactantes.
          </p>
        </header>
        <div class="grid gap-8 md:grid-cols-2">
          <article
            v-for="(project, index) in projects"
            :key="project.title"
            class="group flex h-full flex-col justify-between rounded-3xl border border-white/10 bg-white/5 p-8 transition duration-300 hover:-translate-y-1 hover:border-halloween-orange"
            data-animate="card-flight"
            :data-animate-delay="(index % 3) * 0.12"
            data-animate-scrub="0.8"
            data-animate-end="bottom 45%"
          >
            <div class="space-y-4">
              <h3 class="text-2xl font-semibold text-white">{{ project.title }}</h3>
              <p class="text-white/70">{{ project.description }}</p>
            </div>
            <div class="mt-6 flex flex-wrap items-center gap-3 text-sm text-white/60">
              <span
                v-for="tech in project.stack"
                :key="tech"
                class="rounded-full border border-white/15 px-3 py-1"
              >
                {{ tech }}
              </span>
            </div>
            <a
              :href="project.link"
              class="mt-6 inline-flex items-center gap-2 text-sm font-semibold text-halloween-orange transition group-hover:gap-3"
            >
              Ver estudo de caso
              <span aria-hidden="true">→</span>
            </a>
          </article>
        </div>
      </section>

      <section id="skills" class="js-section border-t border-white/10 py-24">
        <header class="mb-12 space-y-4">
          <h2
            class="text-3xl font-semibold text-white md:text-4xl"
            data-animate="blur-in"
            data-animate-scrub="0.8"
            data-animate-end="+=200"
          >
            Especialidades & Skills
          </h2>
          <p
            class="max-w-2xl text-lg text-white/70"
            data-animate="fade-up"
            data-animate-scrub="0.7"
            data-animate-end="+=220"
          >
            Especialista em tecnologias modernas para desenvolvimento web, com conhecimento profundo em algoritmos e ferramentas de produtividade.
          </p>
        </header>
        <div class="grid gap-6 md:grid-cols-3">
          <div
            v-for="(group, index) in skillGroups"
            :key="group.title"
            class="rounded-3xl border border-white/10 bg-black/60 p-6"
            :data-animate="index % 2 === 0 ? 'tilt-in' : 'scale-pop'"
            :data-animate-delay="index * 0.08"
            data-animate-scrub="0.85"
            data-animate-end="bottom 52%"
          >
            <h3 class="text-sm uppercase tracking-[0.3em] text-white/50">{{ group.title }}</h3>
            <ul class="mt-4 space-y-3 text-white/70">
              <li v-for="item in group.items" :key="item">• {{ item }}</li>
            </ul>
          </div>
        </div>
      </section>

      <section id="experience" class="js-section border-t border-white/10 py-24">
        <header class="mb-12 space-y-4">
          <h2
            class="text-3xl font-semibold text-white md:text-4xl"
            data-animate="blur-in"
            data-animate-scrub="0.8"
            data-animate-end="+=200"
          >
            Experiência
          </h2>
          <p
            class="max-w-2xl text-lg text-white/70"
            data-animate="fade-up"
            data-animate-scrub="0.8"
            data-animate-end="+=240"
          >
            Trajetória profissional focada em crescimento técnico, colaboração em equipes multidisciplinares e entrega de resultados de alta qualidade.
          </p>
        </header>
        <div class="space-y-8">
          <article
            v-for="(entry, index) in timeline"
            :key="entry.role"
            class="rounded-3xl border border-white/10 bg-white/5 p-8"
            :data-animate="index % 2 === 0 ? 'fade-right' : 'drift-in'"
            :data-animate-delay="index * 0.08"
            data-animate-scrub="1"
            data-animate-end="bottom 45%"
          >
            <div class="flex flex-wrap items-baseline justify-between gap-4">
              <div>
                <h3 class="text-2xl font-semibold text-white">{{ entry.role }}</h3>
                <p class="text-sm uppercase tracking-[0.3em] text-white/50">{{ entry.company }}</p>
              </div>
              <span class="text-sm font-semibold text-halloween-orange">{{ entry.period }}</span>
            </div>
            <p class="mt-4 text-white/70">{{ entry.description }}</p>
          </article>
        </div>
      </section>

      <section id="contact" class="js-section border-t border-white/10 py-24 pb-32">
        <div class="grid gap-12 lg:grid-cols-[minmax(0,1fr)_320px]">
          <div class="space-y-6">
            <h2
              class="text-3xl font-semibold text-white md:text-4xl"
              data-animate="blur-in"
              data-animate-scrub="0.8"
              data-animate-end="+=200"
            >
              Pronto para transformar seu próximo projeto?
            </h2>
            <p
              class="text-lg text-white/70"
              data-animate="blur-in"
              data-animate-scrub="0.9"
              data-animate-end="+=220"
            >
              Vamos colaborar em um projeto que impulsione seus objetivos. Compartilhe sua visão e juntos construiremos algo extraordinário.
            </p>
            <a
              href="https://wa.me/5516999934112?text=Olá%20Pedro,%20gostaria%20de%20agendar%20uma%20conversa%20sobre%20um%20projeto."
              target="_blank"
              rel="noopener noreferrer"
              class="inline-block rounded-full bg-gradient-to-r from-halloween-orange via-halloween-purple to-halloween-green px-8 py-4 text-base font-semibold text-black shadow-xl shadow-halloween-orange/30 transition hover:-translate-y-1"
              data-animate="scale-pop"
              data-animate-delay="0.1"
              data-animate-scrub="0.8"
              data-animate-end="bottom 55%"
            >
              Agendar conversa
            </a>
          </div>
          <div class="space-y-6">
            <div
              class="rounded-3xl border border-white/10 bg-black/60 p-6"
              data-animate="tilt-in"
              data-animate-scrub="0.9"
              data-animate-end="bottom 48%"
            >
              <h3 class="text-sm uppercase tracking-[0.3em] text-white/50">Contato direto</h3>
              <ul class="mt-4 space-y-3 text-white/70">
                <li
                  v-for="contactItem in profile.contact"
                  :key="contactItem.label"
                  class="flex items-center gap-2"
                >
                  <span class="text-white/50">{{ contactItem.label }}:</span>
                  <a
                    :href="contactItem.href"
                    class="text-white/80 transition hover:text-white"
                    target="_blank"
                    rel="noopener noreferrer"
                  >
                    {{ contactItem.value }}
                  </a>
                </li>
              </ul>
            </div>
            <div
              class="rounded-3xl border border-white/10 bg-white/5 p-6"
              data-animate="drift-in"
              data-animate-delay="0.12"
              data-animate-scrub="1"
              data-animate-end="bottom 52%"
            >
              <h3 class="text-sm uppercase tracking-[0.3em] text-white/50">Newsletter</h3>
              <p class="mt-3 text-white/70">{{ profile.newsletterText }}</p>
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer class="border-t border-white/10 bg-black/80 py-8">
      <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 px-6 text-sm text-white/50 md:flex-row">
        <p>© {{ currentYear }} {{ profile.name }} — Crafted with Vue, Tailwind CSS & GSAP.</p>
        <div class="flex gap-4">
          <a
            v-for="social in profile.socials"
            :key="social.label"
            :href="social.href"
            class="transition hover:text-white"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ social.label }}
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>
