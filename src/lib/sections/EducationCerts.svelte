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
  }[];

  export let education: {
    level: string;
    degree: string;
    institution: string;
    year: string;
    gpa: string;
  }[];

  export let certifications: {
    name: string;
    issuer: string;
    year: string;
    id: string;
  }[];

  let header: HTMLElement;

  onMount(() => {
    gsap.to(header, {
      text: 'My Professional Journey',
      duration: 2,
      ease: 'power2.inOut',
      scrollTrigger: {
        trigger: header,
        start: 'top 80%',
        toggleActions: 'play none none none',
      }
    });

    gsap.fromTo(
      '.text11',
      { opacity: 0, y: 20 },
      {
        opacity: 0.9,
        y: 0,
        duration: 1,
        scrollTrigger: {
          trigger: '.text11',
          start: 'top 60%',
          toggleActions: 'play none none none',
        },
        stagger: 0.3,
      }
    );
  });
</script>

<section id="journey" class="bg-white py-6 md:py-12 px-4 sm:px-6 lg:px-8 relative">
  <div class="max-w-6xl mx-auto">
    
    <!-- Animated Header -->
    <h2
      bind:this={header}
      class="text-center text-lg sm:text-xl md:text-2xl font-bold text-gray-800 mb-4 md:mb-10 uppercase font-[plexMono]"
    >
      My
    </h2>

    <!-- Responsive Grid / Stack -->
    <div class="flex flex-col gap-4 md:gap-12 lg:grid lg:grid-cols-3 text1">
      
      <!-- Experience -->
      <div>
        <h3 class="text11 text-lg sm:text-xl font-semibold text-gray-900 mb-3 md:mb-6">Experience</h3>
        <div class="space-y-6 text2">
          {#each experience as job}
            <div class="text11 border-l-4 border-gray-200 pl-4">
              <h4 class="text-md sm:text-lg font-bold text-gray-800">{job.title}</h4>
              <p class="text-sm text-gray-600 mb-2">
                {job.company} • <span class="text-gray-500">{job.period}</span>
              </p>
              <ul class="list-disc list-inside space-y-1 text-sm text-gray-700">
                {#each job.responsibilities as res}
                  <li>{res}</li>
                {/each}
              </ul>
            </div>
          {/each}
        </div>
      </div>

      <!-- Education -->
      <div>
        <h3 class="text11 text-lg sm:text-xl font-semibold text-gray-900 mb-3 md:mb-6">Education</h3>
        <div class="space-y-6 text2">
          {#each education as edu}
            <div class="text11 border-l-4 border-gray-200 pl-4">
              <p class="text-sm text-gray-600">{edu.level}</p>
              <h4 class="text-md font-bold text-gray-800">{edu.degree}</h4>
              <p class="text-sm text-gray-600">{edu.institution}</p>
              <p class="text-xs italic text-gray-500">{edu.year} • GPA: {edu.gpa}</p>
            </div>
          {/each}
        </div>
      </div>

      <!-- Certifications -->
      <div>
        <h3 class="text11 text-lg sm:text-xl font-semibold text-gray-900 mb-3 md:mb-6">Certifications</h3>
        <div class="space-y-6 text2">
          {#each certifications as cert}
            <div class="text11 border-l-4 border-gray-200 pl-4">
              <h4 class="text-md sm:text-lg font-bold text-gray-800">{cert.name}</h4>
              <p class="text-sm text-gray-600">{cert.issuer}</p>
              <p class="text-xs text-gray-500">{cert.year} • ID: {cert.id}</p>
            </div>
          {/each}
        </div>
      </div>

    </div>
  </div>
</section>
