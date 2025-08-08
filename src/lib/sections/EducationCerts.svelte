<script lang="ts">
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { TextPlugin } from 'gsap/dist/TextPlugin';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

  gsap.registerPlugin(TextPlugin, ScrollTrigger);

  export let experience: {
    title: string;
    company: string;
    period: string;
    responsibilities: string[];
  }[] = [
    {
      title: "Senior Full Stack Developer",
      company: "Tech Solutions Inc.",
      period: "2022 - Present",
      responsibilities: [
        "Led development of cross-platform mobile and web applications",
        "Architected scalable backend systems serving 100k+ users",
        "Mentored junior developers and established coding standards"
      ]
    },
    {
      title: "Frontend Developer",
      company: "Digital Agency Co.",
      period: "2020 - 2022",
      responsibilities: [
        "Built responsive web applications using React and TypeScript",
        "Collaborated with design team to implement pixel-perfect UIs",
        "Optimized application performance and accessibility"
      ]
    }
  ];

  export let education: {
    level: string;
    degree: string;
    institution: string;
    year: string;
    gpa: string;
  }[] = [
    {
      level: "Bachelor's Degree",
      degree: "Computer Science",
      institution: "University of Technology",
      year: "2020",
      gpa: "3.8"
    }
  ];

  export let certifications: {
    name: string;
    issuer: string;
    year: string;
  }[] = [
    {
      name: "AWS Certified Solutions Architect",
      issuer: "Amazon Web Services",
      year: "2023"
    },
    {
      name: "Google Cloud Professional Developer",
      issuer: "Google Cloud",
      year: "2022"
    },
    {
      name: "React Developer Certification",
      issuer: "Meta",
      year: "2021"
    }
  ];

  let activeTab = 'experience';
  let tabContainer: HTMLElement;

  function setActiveTab(tab: string) {
    activeTab = tab;
  }

  onMount(() => {
    // Simplified header animation only
    gsap.from('.journey-header', {
      opacity: 0,
      y: 30,
      duration: 0.8,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '#journey',
        start: 'top 80%',
        toggleActions: 'play none none none'
      }
    });

    gsap.from('.journey-subtitle', {
      opacity: 0,
      y: 20,
      duration: 0.6,
      ease: 'power3.out',
      delay: 0.2,
      scrollTrigger: {
        trigger: '#journey',
        start: 'top 80%',
        toggleActions: 'play none none none'
      }
    });

    // Simple background parallax
    gsap.to('.bg-accent-journey', {
      scrollTrigger: {
        trigger: '#journey',
        start: 'top bottom',
        end: 'bottom top',
        scrub: true
      },
      y: -30,
      ease: 'none'
    });
  });
</script>

<section id="journey" class="relative bg-slate-100 py-10 lg:py-10 overflow-hidden">
  <!-- Background accents -->
  <div class="bg-accent-journey absolute top-10 left-10 w-72 h-72 bg-blue-100/30 rounded-full blur-3xl"></div>
  <div class="bg-accent-journey absolute bottom-10 right-10 w-80 h-80 bg-purple-100/20 rounded-full blur-3xl"></div>
  
  <!-- Side label for desktop -->
  <div class="absolute -left-0  sm:left-8 top-16">
    <p class="rotate-[-90deg] text-xs font-mono text-neutral-800 tracking-[0.2em] uppercase whitespace-nowrap">
      Journey
    </p>
  </div>

  <div class="mx-auto max-w-6xl px-6 lg:px-12">
    
    <!-- Header -->
    <div class="text-center mb-2 lg:mb-2">
      <h2 class="journey-header text-3xl lg:text-4xl xl:text-5xl font-light text-gray-900 mb-4">
        Professional Journey
      </h2>
      <p class="journey-subtitle text-lg text-gray-600 max-w-2xl mx-auto">
        A timeline of growth, learning, and meaningful contributions
      </p>
    </div>

    <!-- Mobile/Desktop Adaptive Navigation -->
    <div class="mb-8 lg:mb-8">
      <!-- Mobile: Dropdown-style tabs -->
      <div class="block sm:hidden">
        <select 
          bind:value={activeTab} 
          on:change={() => setActiveTab(activeTab)}
          class="w-full px-4 py-3 bg-white border border-gray-200 rounded-xl text-gray-900 font-medium focus:outline-none focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500"
        >
          <option value="experience">Experience</option>
          <option value="education">Education</option>
          <option value="certifications">Certifications</option>
        </select>
      </div>

      <!-- Desktop: Tab buttons -->
      <div class="hidden sm:flex justify-center space-x-1 bg-white/70 backdrop-blur-md p-1 rounded-2xl border border-gray-200/70 max-w-md mx-auto">
        <button
          class="flex-1 px-6 py-3 text-sm font-medium rounded-xl transition-all duration-300 {activeTab === 'experience' ? 'bg-white text-gray-900 shadow-sm' : 'text-gray-500 hover:text-gray-700'}"
          on:click={() => setActiveTab('experience')}
        >
          Experience
        </button>
        <button
          class="flex-1 px-6 py-3 text-sm font-medium rounded-xl transition-all duration-300 {activeTab === 'education' ? 'bg-white text-gray-900 shadow-sm' : 'text-gray-500 hover:text-gray-700'}"
          on:click={() => setActiveTab('education')}
        >
          Education
        </button>
        <button
          class="flex-1 px-6 py-3 text-sm font-medium rounded-xl transition-all duration-300 {activeTab === 'certifications' ? 'bg-white text-gray-900 shadow-sm' : 'text-gray-500 hover:text-gray-700'}"
          on:click={() => setActiveTab('certifications')}
        >
          Certifications
        </button>
      </div>
    </div>

    <!-- Content Area -->
    <div class="min-h-[400px]">
      
      <!-- Experience Content -->
      {#if activeTab === 'experience'}
        <div class="space-y-6 lg:space-y-8">
          {#each experience as job, index}
            <div class="group">
              <div class="bg-white/80 backdrop-blur-sm rounded-2xl p-6 lg:p-8 border border-gray-200/50 hover:shadow-lg hover:shadow-gray-200/50 transition-all duration-300">
                <div class="flex flex-col lg:flex-row lg:items-start lg:justify-between gap-4 lg:gap-6">
                  <div class="flex-1">
                    <div class="flex items-start gap-4">
                      <div class="flex-shrink-0 w-12 h-12 bg-gradient-to-br from-blue-100 to-blue-200 rounded-xl flex items-center justify-center">
                        <div class="w-6 h-6 bg-blue-600 rounded-md"></div>
                      </div>
                      <div class="flex-1">
                        <h3 class="text-xl font-semibold text-gray-900 mb-1">{job.title}</h3>
                        <p class="text-blue-600 font-medium mb-2">{job.company}</p>
                        <p class="text-sm text-gray-500 mb-4">{job.period}</p>
                      </div>
                    </div>
                    <div class="ml-16">
                      <ul class="space-y-2">
                        {#each job.responsibilities as responsibility}
                          <li class="flex items-start gap-3 text-gray-700">
                            <div class="flex-shrink-0 w-1.5 h-1.5 bg-gray-400 rounded-full mt-2"></div>
                            <span class="text-sm leading-relaxed">{responsibility}</span>
                          </li>
                        {/each}
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          {/each}
        </div>
      {/if}

      <!-- Education Content -->
      {#if activeTab === 'education'}
        <div class="space-y-6 lg:space-y-6">
          {#each education as edu, index}
            <div class="group">
              <div class="bg-white/80 backdrop-blur-sm rounded-2xl p-6 lg:p-8 border border-gray-200/50 hover:shadow-lg hover:shadow-gray-200/50 transition-all duration-300">
                <div class="flex items-start gap-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-gradient-to-br from-purple-100 to-purple-200 rounded-xl flex items-center justify-center">
                    <div class="w-6 h-6 bg-purple-600 rounded-md"></div>
                  </div>
                  <div class="flex-1">
                    <span class="inline-block px-3 py-1 bg-purple-100 text-purple-700 text-xs font-medium rounded-full mb-3">
                      {edu.level}
                    </span>
                    <h3 class="text-xl font-semibold text-gray-900 mb-2">{edu.degree}</h3>
                    <p class="text-purple-600 font-medium mb-2">{edu.institution}</p>
                    <div class="flex flex-wrap gap-4 text-sm text-gray-500">
                      <span>{edu.year}</span>
                      <span>•</span>
                      <span class="font-bold italic">{edu.gpa}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          {/each}
        </div>
      {/if}

      <!-- Certifications Content -->
      {#if activeTab === 'certifications'}
        <div class="grid gap-6 md:grid-cols-2">
          {#each certifications as cert, index}
            <div class="group">
              <div class="bg-white/80 backdrop-blur-sm rounded-2xl p-6 border border-gray-200/50 hover:shadow-lg hover:shadow-gray-200/50 transition-all duration-300 h-full">
                <div class="flex items-start gap-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-gradient-to-br from-green-100 to-green-200 rounded-xl flex items-center justify-center">
                    <div class="w-6 h-6 bg-green-600 rounded-md"></div>
                  </div>
                  <div class="flex-1">
                    <h3 class="text-lg font-semibold text-gray-900 mb-2">{cert.name}</h3>
                    <p class="text-green-600 font-medium mb-1">{cert.issuer}</p>
                    <p class="text-sm text-gray-500">{cert.year}</p>
                  </div>
                </div>
              </div>
            </div>
          {/each}
        </div>
      {/if}

    </div>
  </div>
</section>