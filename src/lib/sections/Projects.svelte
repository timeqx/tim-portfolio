<script lang="ts">
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

  export let projects;

  let currentIndex = 0;
  let mounted = false;
  let containerRef;
  let projectRefs = [];

  onMount(() => {
    mounted = true;
    gsap.registerPlugin(ScrollTrigger);

    // Initial animation for the section
    gsap.fromTo('.projects-header', 
      { opacity: 0, y: 50 }, 
      { 
        opacity: 1, 
        y: 0, 
        duration: 0.8,
        scrollTrigger: {
          trigger: '.projects-header',
          start: 'top 80%',
          toggleActions: 'play none none none'
        }
      }
    );

    // Stagger animation for project cards
    gsap.fromTo('.project-card', 
      { opacity: 0, y: 80, scale: 0.9 }, 
      { 
        opacity: 1, 
        y: 0,
        scale: 1,
        duration: 0.8,
        stagger: 0.2,
        scrollTrigger: {
          trigger: '.projects-container',
          start: 'top 70%',
          toggleActions: 'play none none none'
        }
      }
    );

    return () => ScrollTrigger.getAll().forEach(trigger => trigger.kill());
  });

  function goToProject(index: number) {
    if (index !== currentIndex) {
      gsap.to('.project-card', {
        opacity: 0.3,
        scale: 0.95,
        duration: 0.3,
        ease: 'power2.out'
      });

      setTimeout(() => {
        currentIndex = index;
        gsap.to('.project-card', {
          opacity: 1,
          scale: 1,
          duration: 0.5,
          ease: 'power2.out'
        });
      }, 300);
    }
  }

  function nextProject() {
    if (currentIndex < projects.length - 1) {
      goToProject(currentIndex + 1);
    }
  }

  function prevProject() {
    if (currentIndex > 0) {
      goToProject(currentIndex - 1);
    }
  }

  $: currentProject = projects[currentIndex];
</script>

<style>
  .device-mockup {
    position: relative;
    background: linear-gradient(145deg, #2a2a2a 0%, #1a1a1a 100%);
    border-radius: 24px;
    box-shadow: 
      0 25px 50px rgba(0, 0, 0, 0.5),
      0 0 0 1px rgba(255, 255, 255, 0.1),
      inset 0 1px 0 rgba(255, 255, 255, 0.2);
  }

  .browser-mockup {
    padding: 40px 20px 20px;
  }

  .browser-mockup::before {
    content: '';
    position: absolute;
    top: 12px;
    left: 20px;
    display: flex;
    align-items: center;
    gap: 8px;
    width: 54px;
    height: 12px;
    background: 
      radial-gradient(circle, #ff5f56 0%, #ff5f56 33%, transparent 33%),
      radial-gradient(circle, #ffbd2e 0%, #ffbd2e 33%, transparent 33%),
      radial-gradient(circle, #27ca3f 0%, #27ca3f 33%, transparent 33%);
    background-size: 12px 12px;
    background-position: 0 0, 18px 0, 36px 0;
    background-repeat: no-repeat;
  }

  .phone-mockup {
    padding: 12px 12px 18px 12px;
    width: 300px;
    height: 660px;
  }

  .phone-mockup::before {
    content: '';
    position: absolute;
    top: 5px;
    left: 50%;
    transform: translateX(-50%);
    width: 40px;
    height: 3px;
    background: rgba(255, 255, 255, 0.3);
    border-radius: 2px;
  }

  .phone-mockup::after {
    content: '';
    position: absolute;
    bottom: 8px;
    left: 50%;
    transform: translateX(-50%);
    width: 60px;
    height: 4px;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 2px;
  }

  .project-screen {
    width: 100%;
    height: 100%;
    border-radius: 8px;
    overflow: hidden;
    background: #f8fafc;
    box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.1);
  }

  .mobile-screens {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .mobile-screen {
    width: 180px;
    height: 390px ;
  }

  .tech-tag {
    background: linear-gradient(135deg, rgba(148, 113, 203, 0.1) 0%, rgba(179, 102, 115, 0.1) 100%);
    border: 1px solid rgba(148, 113, 203, 0.2);
    color: #7c3aed;
    transition: all 0.3s ease;
  }

  .tech-tag:hover {
    background: rgba(148, 113, 203, 0.2);
    transform: translateY(-2px);
  }

  .floating-nav {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.2);
  }

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
  }

  .float-animation {
    animation: float 6s ease-in-out infinite;
  }

  @media (max-width: 768px) {
    .mobile-screen {
      width: 120px;
      height: 240px;
    }
    
    .phone-mockup {
      width: 200px;
      height: 400px;
    }
  }
</style>

<section class="relative min-h-screen bg-gradient-to-br from-neutral-50 to-neutral-100 py-10">
 
  <div class="absolute -left-8 sm:left-8 top-16">
    <p class="rotate-[-90deg] text-xs font-mono text-neutral-800 tracking-[0.2em] uppercase whitespace-nowrap">
       Selected Works
    </p>
  </div>

  <div class="max-w-7xl mx-auto px-6">
    <!-- Header -->
    <div class="projects-header text-center mb-16">
      <p class="text-sm font-mono text-violet-600 tracking-widest uppercase mb-4">
        Portfolio
      </p>
      <h2 class="text-3xl md:text-6xl font-light text-neutral-900 mb-6">
        Featured Projects
      </h2>
      <p class="text-lg text-neutral-600 max-w-2xl mx-auto">
        A collection of web and mobile applications showcasing modern development practices
      </p>
    </div>

    <!-- Project Showcase -->
    {#if currentProject}
      <div class="projects-container grid lg:grid-cols-2 gap-16 items-center mb-8">
        <!-- Device Container -->
        <div class="flex justify-center">
          {#if currentProject.type === 'web'}
            <!-- Browser Mockup -->
            <div class="device-mockup browser-mockup max-w-2xl w-full float-animation">
              <div class="project-screen">
                <img 
                  src={currentProject.image} 
                  alt={currentProject.title}
                  class="w-full h-full object-cover object-top"
                  loading="lazy"
                />
              </div>
            </div>
          {:else if currentProject.type === 'mobile'}
            <!-- Mobile Mockups -->
            <div class="mobile-screens">
              {#each [
                { src: currentProject.image, alt: `${currentProject.title} - Main Screen` },
                { src: currentProject.image2, alt: `${currentProject.title} - Feature Screen` },
                { src: currentProject.image3, alt: `${currentProject.title} - Detail Screen` }
              ] as screen, screenIndex}
                <div class="device-mockup phone-mockup mobile-screen float-animation" style="animation-delay: {screenIndex * 0.5}s">
                  <div class="project-screen">
                    {#if screen.src}
                      <img 
                        src={screen.src} 
                        alt={screen.alt}
                        class="w-full h-full object-cover object-top"
                        loading="lazy"
                      />
                    {:else}
                      <!-- Fallback placeholder if image doesn't exist -->
                      <div class="w-full h-full bg-gradient-to-br from-neutral-100 to-neutral-200 flex items-center justify-center">
                        <div class="text-center text-neutral-400">
                          <svg class="w-12 h-12 mx-auto mb-2" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 18h.01M8 21h8a1 1 0 001-1V4a1 1 0 00-1-1H8a1 1 0 00-1 1v16a1 1 0 001 1z"/>
                          </svg>
                          <p class="text-xs">Screen {screenIndex + 1}</p>
                        </div>
                      </div>
                    {/if}
                  </div>
                </div>
              {/each}
            </div>
          {/if}
        </div>

        <!-- Project Details -->
        <div class="space-y-8">
          <div>
            <div class="flex items-center gap-3 mb-4">
              <span class="px-3 py-1 bg-violet-100 text-violet-700 text-sm font-medium rounded-full">
                {currentProject.type === 'web' ? 'Web Application' : 'Mobile App'}
              </span>
              <span class="text-neutral-400 text-sm">
                {currentIndex + 1} of {projects.length}
              </span>
            </div>
            
            <h3 class="text-3xl font-light text-neutral-900 mb-4 leading-tight">
              {currentProject.title}
            </h3>
            
            <p class="text-neutral-600 leading-relaxed text-lg">
              {currentProject.description}
            </p>
          </div>

          <!-- Tech Stack -->
          <div>
            <p class="text-sm font-mono text-neutral-500 uppercase tracking-widest mb-4">
              Technologies Used
            </p>
            <div class="flex flex-wrap gap-3">
              {#each currentProject.tech as tech}
                <span class="tech-tag px-4 py-2 rounded-full text-sm font-medium">
                  {tech}
                </span>
              {/each}
            </div>
          </div>

          <!-- Actions -->
          <div class="flex gap-4">
            {#if currentProject.github}
              <a 
                href={currentProject.github}
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center gap-2 px-6 py-3 bg-neutral-900 text-white rounded-full hover:bg-neutral-800 transition-all duration-300 hover:scale-105"
              >
                <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                </svg>
                View Code
              </a>
            {/if}
            
            {#if currentProject.demo}
              <a 
                href={currentProject.demo}
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center gap-2 px-6 py-3 border border-neutral-300 text-neutral-700 rounded-full hover:bg-neutral-50 transition-all duration-300 hover:scale-105"
              >
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
                </svg>
                Live Demo
              </a>
            {/if}
          </div>
        </div>
      </div>
    {/if}

    <!-- Project Navigation -->
    <div class="flex justify-center">
      <div class="floating-nav rounded-2xl p-6 flex items-center gap-6">
        <!-- Navigation Dots -->
        <div class="flex gap-3 bg-[#131010] px-3 py-2 rounded-lg w-auto">
          {#each projects as _, index}
            <button
              on:click={() => goToProject(index)}
              class="w-3 h-3 rounded-full transition-all duration-300 {currentIndex === index ? 'bg-[#FAC050ff] scale-125' : 'bg-neutral-300 hover:bg-neutral-400'}"
              aria-label="View project {index + 1}"
            ></button>
          {/each}
        </div>
		

        <!-- Arrow Navigation -->
        <div class="flex gap-2">
          <button
            on:click={prevProject}
            disabled={currentIndex === 0}
            class="p-2 rounded-full border border-neutral-200 text-[#131010] hover:bg-neutral-300 disabled:opacity-30 disabled:cursor-not-allowed transition-all duration-300"
            aria-label="Previous project"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/>
            </svg>
          </button>
          
          <button
            on:click={nextProject}
            disabled={currentIndex === projects.length - 1}
            class="p-2 rounded-full border border-neutral-200 text-[#131010] hover:bg-neutral-300 disabled:opacity-30 disabled:cursor-not-allowed transition-all duration-300"
            aria-label="Next project"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Quick Project Grid -->
    <div class="mt-5 grid md:grid-cols-2 lg:grid-cols-4 gap-6">
      {#each projects as project, index}
        <button
          on:click={() => goToProject(index)}
          class="project-card group p-3 bg-white rounded-2xl shadow-sm hover:shadow-xl transition-all duration-500 text-left border border-neutral-100 hover:border-violet-200 {currentIndex === index ? 'ring-2 ring-violet-200 bg-violet-50' : ''}"
        >
		<div class="flex flex-row gap-2 justify-center">
          <div class="w-12 h-12 bg-gradient-to-br from-violet-500 to-purple-600 rounded-xl mb-4 flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
            {#if project.type === 'web'}
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9v-9m0-9v9m0 9c-5 0-9-4-9-9s4-9 9-9"/>
              </svg>
            {:else}
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a1 1 0 001-1V4a1 1 0 00-1-1H8a1 1 0 00-1 1v16a1 1 0 001 1z"/>
              </svg>
            {/if}
          </div>
          
          <h4 class="font-medium text-neutral-900 mb-2 group-hover:text-violet-700 transition-colors">
            {project.title.length > 32 ? project.title.substring(0, 32) + '...' : project.title}
          </h4>
          </div>
          <p class="text-sm text-neutral-600 mb-3 line-clamp-2">
            {project.description.substring(0, 80)}...
          </p>
          
          <div class="flex gap-1 flex-wrap">
            {#each project.tech.slice(0, 2) as tech}
              <span class="text-xs px-2 py-1 bg-neutral-100 text-neutral-600 rounded">
                {tech}
              </span>
            {/each}
            {#if project.tech.length > 2}
              <span class="text-xs px-2 py-1 bg-neutral-100 text-neutral-600 rounded">
                +{project.tech.length - 2}
              </span>
            {/if}
          </div>
        </button>
      {/each}
    </div>
  </div>
</section>