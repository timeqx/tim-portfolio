<script lang="ts">
import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

  export let techStack;

  let component: HTMLElement;

  gsap.registerPlugin(ScrollTrigger);

  const repeat = [1, 2, 3, 4, 5];

  onMount(() => {
    const t1 = gsap.timeline({
      scrollTrigger: {
        trigger: component,
        start: 'top bottom',
        end: 'bottom top',
        scrub: 4,

        markers:true
      }
    });
  t1.fromTo(".tech-row", {
    x:(index)=>{
      return index % 2 === 0 ? gsap.utils.random(600,400) : gsap.utils.random(-600,-400)
    }
  }, {
x:(index)=>{
      return index % 2 === 0 ? gsap.utils.random(-600,-400) : gsap.utils.random(600,400)
    },
    ease: 'power1.inOut'
  })

});
</script>

<section class=" px-6 py-3 bg-[#131010] overflow-hidden" bind:this={component}>
  <div class="max-w-6xl p-4 mx-auto">
    <h2 class="text-6xl font-semibold font-[plexMono] text-gray-200 mb-8 tracking-tight  text-left opacity-80">What I Use</h2>
      {#each techStack as category}
    <div class=" tech-row mb-4 flex items-center justify-center">

          {#each Array(15) as _, index}
            <div class="flex items-center justify-center" >
              {#each category.skills as skill}
                <span class="tech-item text-5xl text-center font-bold uppercase tracking-tighter  whitespace-nowrap " style="color: {index === 7 && category.color ? category.color : '#292929'}" aria-label={skill || undefined}>
                {skill}◦
                </span>
              {/each}
            </div>
          {/each}
       </div>
      {/each}
  </div>
</section>
