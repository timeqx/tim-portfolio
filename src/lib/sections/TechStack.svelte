<script lang="ts">
import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

  export let techStack;

 

  gsap.registerPlugin(ScrollTrigger);

  const repeat = [1, 2, 3, 4, 5];

  onMount(() => {
    const t1 = gsap.timeline({
      scrollTrigger: {
        trigger: 'section',
        start: 'top bottom',
        end: 'bottom top',
        scrub: 4,

        markers:true,
      }
    });
 

});
</script>

<section class="mb-16 px-6 py-3 bg-[#131010]">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-3xl font-bold text-gray-900  text-center">Tech Stack</h2>
      {#each techStack as category}
    <div class=" tech-row mb-2 flex items-center justify-center">

          {#each Array(10) as _, index}
            <div class="flex gap-1 items-center justify-center" >
              {#each category.skills as skill}
                <span class="tech-item text-5xl text-center font-extrabold uppercase tracking-tighter  whitespace-nowrap " style="color: {index === 5 && category.color ? category.color : '#292929'}" aria-label={skill || undefined}>
                {skill} •
                </span>
              {/each}
            </div>
          {/each}
       </div>
      {/each}
  </div>
</section>
