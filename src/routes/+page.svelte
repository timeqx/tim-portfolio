<!-- src/routes/+page.svelte -->
<script lang="ts">
  import Hero from '$lib/sections/Hero.svelte';
  import Iam from '$lib/sections/Iam.svelte';
  import TechStack from '$lib/sections/TechStack.svelte';
  import Gallery from '$lib/sections/Gallery.svelte';
  import Projects from '$lib/sections/Projects.svelte';
  import EducationCerts from '$lib/sections/EducationCerts.svelte';
  import Contact from '$lib/sections/Contact.svelte';
  import Footer from '$lib/sections/Footer.svelte';
  import HeroCube from '$lib/sections/HeroCube.svelte';
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';

  import { profile } from '$lib/data/profile';
  import { techStack } from '$lib/data/techStack';
  import { projects } from '$lib/data/projects';
  import { education } from '$lib/data/education';
  import { certifications } from '$lib/data/certifications';
  import { experience } from '$lib/data/experience';

  let mounted = false;
  let activeSection = 'hero';
  let isMenuOpen = false;
  let scrollY = 0;
  let navRef;
  let scrollProgress = 0;

  const sections = [
    { id: 'hero', label: 'Home', color: '#9471CB' },
    { id: 'about', label: 'About', color: '#8F4816' },
    { id: 'techStackS', label: 'Stack', color: '#FAC050' },
    { id: 'projectsS', label: 'Work', color: '#B36673' },
    { id: 'journey', label: 'Journey', color: '#9471CB' },
    { id: 'contact', label: 'Contact', color: '#634a9b' }
  ];

  onMount(() => {
  mounted = true;
  
  const observer = new IntersectionObserver(
    (entries) => {
  
      const sortedEntries = entries.sort((a, b) => b.intersectionRatio - a.intersectionRatio);
      
      for (const entry of sortedEntries) {
        if (entry.isIntersecting && entry.intersectionRatio > 0.3) {
          activeSection = entry.target.id;
          break; 
        }
      }
    },
    { 
      threshold: [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0],
      rootMargin: '-100px 0px -100px 0px' 
    }
  );

  const manualSectionDetection = () => {
    if (!browser) return;
    
    const scrollPosition = window.scrollY + 200; 
    let currentSection = 'hero';
    
    sections.forEach(section => {
      const element = document.getElementById(section.id);
      if (element) {
        const offsetTop = element.offsetTop;
        const offsetBottom = offsetTop + element.offsetHeight;
        
        if (scrollPosition >= offsetTop && scrollPosition < offsetBottom) {
          currentSection = section.id;
        }
      }
    });
    
    if (currentSection !== activeSection) {
      activeSection = currentSection;
    }
  };


  sections.forEach(section => {
    const element = document.getElementById(section.id);
    if (element) {
      observer.observe(element);
    }
  });

  const updateScrollProgress = () => {
    if (browser && document.documentElement) {
      const scrollTop = window.scrollY;
      const docHeight = document.documentElement.scrollHeight - window.innerHeight;
      scrollProgress = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0;
      
     
      manualSectionDetection();
    }
  };


  updateScrollProgress();

  let ticking = false;
  const handleScroll = () => {
    if (!ticking) {
      requestAnimationFrame(() => {
        updateScrollProgress();
        ticking = false;
      });
      ticking = true;
    }
  };

  window.addEventListener('scroll', handleScroll, { passive: true });

  return () => {
    observer.disconnect();
    window.removeEventListener('scroll', handleScroll);
  };
});

  function scrollToSection(sectionId: string) {
    activeSection = sectionId;
    isMenuOpen = false;
    
    const element = document.getElementById(sectionId);
    if (element) {
      const offsetTop = element.offsetTop - 65;
      window.scrollTo({
        top: offsetTop,
        behavior: 'smooth'
      });
    }
  }

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  // Calculate nav background opacity based on scroll
  $: navOpacity = Math.min(scrollY / 100, 0.95);
</script>

<svelte:head>
  <title>Timothy Osorio • Full Stack Developer</title>
  <meta name="description" content="{profile.name} - {profile.title} Portfolio showcasing modern web and mobile development" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</svelte:head>

<svelte:window bind:scrollY />

<style>
  @keyframes fadeInUp {
    from {
      opacity: 0;
      transform: translateY(30px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes slideIn {
    from {
      transform: translateX(-100%);
      opacity: 0;
    }
    to {
      transform: translateX(0);
      opacity: 1;
    }
  }

  .nav-blur {
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .nav-item {
    position: relative;
    transition: all 0.3s cubic-bezier(0.23, 1, 0.32, 1);
  }

  .nav-item::after {
    content: '';
    position: absolute;
    bottom: -8px;
    left: 50%;
    width: 0;
    height: 2px;
    background: var(--accent-color, #9471CB);
    transform: translateX(-50%);
    transition: width 0.3s ease;
    border-radius: 1px;
  }

  .nav-item.active::after {
    width: 24px;
  }

  .mobile-menu {
    background: rgba(19, 16, 16, 0.98);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    animation: slideIn 0.3s ease-out;
  }

  .section-wrapper {
    position: relative;
    opacity: 0;
    animation: fadeInUp 0.8s ease-out forwards;
  }

  .section-wrapper:nth-child(1) { animation-delay: 0.1s; }
  .section-wrapper:nth-child(2) { animation-delay: 0.2s; }
  .section-wrapper:nth-child(3) { animation-delay: 0.3s; }
  .section-wrapper:nth-child(4) { animation-delay: 0.4s; }
  .section-wrapper:nth-child(5) { animation-delay: 0.5s; }
  .section-wrapper:nth-child(6) { animation-delay: 0.6s; }

  .hero-container {
    position: relative;
    overflow: hidden;
  }

  @media (max-width: 768px) {
    .nav-item::after {
      display: none;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .section-wrapper, .mobile-menu {
      animation: none;
      opacity: 1;
    }
    .nav-item {
      transition: none;
    }
  }
</style>

<div class="relative min-h-screen bg-[#131010]">
  <!-- Enhanced Navigation -->
  <nav 
    bind:this={navRef}
    class="fixed top-0 w-full z-[999] nav-blur transition-all duration-300"
    style="background-color: rgba(19, 16, 16, {navOpacity})"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <button 
          on:click={() => scrollToSection('hero')}
          class="font-mono text-lg font-medium text-white hover:text-[#9471CB] transition-colors duration-300"
        >
          <span class="text-[#9471CB]">&lt;</span>
          {profile.name.split(' ')[0].toLowerCase()}
          <span class="text-[#9471CB]">/&gt;</span>
        </button>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          {#each sections as section}
            <button
              on:click={() => scrollToSection(section.id)}
              class="nav-item text-sm font-medium text-neutral-400 hover:text-white transition-colors duration-300 {activeSection === section.id ? 'active text-white' : ''}"
              style="--accent-color: {section.color}"
            >
              {section.label}
            </button>
          {/each}
        </div>

        <!-- Mobile Menu Button -->
        <button
          on:click={toggleMenu}
          class="md:hidden p-2 text-neutral-400 hover:text-white transition-colors duration-300"
          aria-label="Toggle menu"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            {#if isMenuOpen}
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            {:else}
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            {/if}
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    {#if isMenuOpen}
      <div class="mobile-menu md:hidden absolute top-full left-0 w-full">
        <div class="px-4 py-6 space-y-4">
          {#each sections as section}
            <button
              on:click={() => scrollToSection(section.id)}
              class="block w-full text-left px-4 py-3 text-neutral-400 hover:text-white hover:bg-white/5 rounded-lg transition-all duration-300 {activeSection === section.id ? 'text-white bg-white/10' : ''}"
            >
              <span class="text-sm font-medium">{section.label}</span>
              {#if activeSection === section.id}
                <div class="w-2 h-2 bg-[{section.color}] rounded-full mt-1"></div>
              {/if}
            </button>
          {/each}
        </div>
      </div>
    {/if}
  </nav>

  <!-- Page Content -->
  <main>
    <!-- Hero Section with Cube Background -->
    <div id="hero" class="hero-container section-wrapper">
      {#if mounted}
        <div class="absolute inset-0 z-30">
          <HeroCube />
        </div>
      {/if}
      <div class="relative z-20">
        <Hero {profile} />
      </div>
    </div>

    <!-- About Section -->
    <div id="about" class="section-wrapper">
      <Iam {profile} />
    </div>

    <!-- Tech Stack Section -->
    <div id="techStackS" class="section-wrapper">
      <TechStack {techStack} />
    </div>

    <!-- Projects Section -->
    <div id="projectsS" class="section-wrapper">
      <Projects {projects} />
    </div>

    <!-- Education & Experience Section -->
    <div id="journey" class="section-wrapper">
      <EducationCerts {experience} {education} {certifications} />
    </div>

    <!-- Contact Section -->
    <div id="contact" class="section-wrapper">
      <Contact {profile} />
    </div>

    <!-- Footer -->
    <div class="section-wrapper">
      <Footer {profile} />
    </div>
  </main>

  <!-- Scroll Progress Indicator -->
  {#if browser}
    <div 
      class="fixed top-16 left-0 h-0.5 bg-gradient-to-r from-[#9471CB] via-[#B36673] to-[#FAC050] z-[998] transition-all duration-150"
      style="width: {scrollProgress}%"
    ></div>
  {/if}
</div>