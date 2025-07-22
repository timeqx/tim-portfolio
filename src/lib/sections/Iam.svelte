<script lang="ts">
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
  import { TextPlugin } from 'gsap/dist/TextPlugin';

  export let profile;

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger, TextPlugin);

    gsap.fromTo(
      '.photo1',
      { opacity: 0.9 },
      {
        scrollTrigger: {
          trigger: '.photo1',
          start: 'top 40%',
          end: 'bottom center',
          scrub: true
        },
        opacity: 0,
        ease: 'none'
      }
    );
    gsap.fromTo(
      '.photo2',
      { opacity: 0 },
      {
        scrollTrigger: {
          trigger: '.photo1',
          start: 'top 40%',
          end: 'top 90%',
          scrub: true
        },
        opacity: 0.9,
        ease: 'none'
      }
    );

    gsap.fromTo(
      '.text1',
      { opacity: 0, y: 20 },
      {
        scrollTrigger: {
          trigger: '.text1',
          start: 'top 80%',
          end: 'top 80%',
          toggleActions: 'play none none none'
        },
        opacity: 0.9,
        y: 0,
        duration: 1
      }
    );
    gsap.fromTo(
      '.text2',
      { opacity: 0, y: 20 },
      {
        scrollTrigger: {
          trigger: '.text1',
          start: 'top 80%',
          end: 'bottom 30%',
          toggleActions: 'play none none none'
        },
        stagger: 0.3,
        opacity: 0.9,
        y: 0,
        delay: 0.5,
        duration: 1
      }
    );
  });
</script>

<section id="about" class="relative bg-gradient-to-br from-slate-100 to-gray-200 py-20 text-gray-900">
    <div class=" md:block absolute md:left-16 left-0 top-20">
    <p class="rotate-[-90deg] md:text-xl text-sm text-gray-500 font-semibold tracking-widest font-[plexMono] uppercase text-left ">
      WHO I AM
    </p>
  </div>
  <div class="mx-auto max-w-6xl px-6 md:px-6">
   
    <div class="flex flex-col-reverse lg:flex-row items-center justify-between gap-12">
      <!-- Left: Text Content -->
      <div class="w-full lg:w-1/2">
        <p class="text1 font-serif text-2xl md:text-3xl font-semibold tracking-widest text-[#5A30B6ff] mb-2 text-center lg:text-left">
          / ' i am, ' /
        </p>

        <h2 class="text2 text-3xl md:text-4xl font-light tracking-widest text-black mb-4 text-center lg:text-left">
          Timothy Osorio,
        </h2>

        <div class="flex flex-wrap justify-center lg:justify-start gap-3 mb-4">
          <span class="text2 badge badge-ghost text-sm font-medium px-3 py-2">Developer</span>
          <span class="text2 italic text-gray-600">disciplined</span>
          <span class="text2 italic text-gray-600">adaptable</span>
          <span class="text2 italic text-gray-600">future-minded</span>
        </div>

        <div class="text2 text-base leading-relaxed space-y-4 text-justify font-light">
          <p>
            I'm a full stack developer with a knack for building
            <strong class="text-black">timeless, cross-platform experiences</strong>.
            Whether it's websites, software, or mobile apps, I craft solutions with elegance,
            performance, and precision.
          </p>
          <p>
            From UI to backend, cloud to device — I design systems that not only work well, but
            <strong class="text-black">feel effortless to use</strong>.
          </p>
        </div>
      </div>

      <!-- Right: Images -->
      <div class="w-full lg:w-1/2 flex justify-center">
        <div class="relative items-center justify-center flex h-[22rem] w-56 sm:h-[24rem] sm:w-[18rem] rounded-xl">
          <img
            src="/holo.jpg"
            alt="Background"
            class="absolute sm:max-h-full max-h-[21rem] h-full max-w-[16rem] w-full rounded-xl object-cover  z-10"
          />
          <img
            src="/prof2.JPG"
            alt="Timothy Osorio"
            class="photo2 absolute sm:max-h-full max-h-[21rem] h-full max-w-[16rem]  w-full rounded-xl object-contain shadow-2xl z-20"
          />
          <img
            src="/prof1.JPG"
            alt="Timothy Osorio"
            class="photo1 absolute sm:max-h-full max-h-[21rem] h-full max-w-[16rem]  w-full rounded-xl object-contain shadow-2xl z-30"
          />
        </div>
      </div>
    </div>
  </div>
</section>
