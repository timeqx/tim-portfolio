<script lang="ts">
  import { onMount } from 'svelte';
  import {gsap} from 'gsap';
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
    // Text animation trigger
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

    // Text block animation
    gsap.fromTo(
      '.text1',
      { opacity: 0, y: 20 },
      {
        opacity: 0.9,
        y: 0,
        duration: 1,
        scrollTrigger: {
          trigger: '.text1',
          start: 'top 80%',
          toggleActions: 'play none none none',
        }
      }
    );

   
  });
</script>

<section id="journey" class="bg-white py-24 px-6">
  <div class="max-w-6xl mx-auto">
    <!-- Animated Section Title -->
    <h2
      bind:this={header}
      class="text-3xl md:text-4xl font-bold text-center text-gray-800 mb-16 font-[plexMono]"
    >
      <!-- Will be replaced by TextPlugin -->
      My
    </h2>

    <div class="grid md:grid-cols-3 gap-12 text1">
      <!-- Experience -->
      <div>
        <h3 class="text1 text-2xl font-semibold text-gray-900 mb-6">Experience</h3>
        <div class="space-y-6 text2">
          {#each experience as job}
            <div class="text1 border-l-4 border-gray-200 pl-5">
              <h4 class="text-lg font-bold text-gray-800">{job.title}</h4>
              <p class="text-gray-600 text-sm mb-2">
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
        <h3 class="text1 text-2xl font-semibold text-gray-900 mb-6">Education</h3>
        <div class="space-y-6 text2">
          {#each education as edu}
            <div class="text1 border-l-4 border-gray-200 pl-5">
              <p class="text-sm text-gray-600">{edu.level}</p>
              <h4 class="text-lg font-bold text-gray-800">{edu.degree}</h4>
              <p class="text-sm text-gray-600">{edu.institution}</p>
              <p class="text-xs text-gray-500">{edu.year} • {edu.gpa}</p>
            </div>
          {/each}
        </div>
      </div>

      <!-- Certifications -->
      <div>
        <h3 class="text1 text-2xl font-semibold text-gray-900 mb-6">Certifications</h3>
        <div class="space-y-6 text2">
          {#each certifications as cert}
            <div class="text1 border-l-4 border-gray-200 pl-5">
              <h4 class="text-lg font-bold text-gray-800">{cert.name}</h4>
              <p class="text-sm text-gray-600">{cert.issuer}</p>
              <p class="text-xs text-gray-500">{cert.year} • ID: {cert.id}</p>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>
