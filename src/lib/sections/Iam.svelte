<script lang="ts">
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
  import { TextPlugin } from 'gsap/dist/TextPlugin';

  export let profile;

  function scrollToSection(sectionId: string) {
    const element = document.querySelector(sectionId);
    if (element) {
      element.scrollIntoView({ 
        behavior: 'smooth',
        block: 'start'
      });
    }
  }

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger, TextPlugin);

    // Photo transition animation - smoother and more refined
    gsap.fromTo(
      '.photo1',
      { opacity: 1, scale: 1 },
      {
        scrollTrigger: {
          trigger: '.photo-container',
          start: 'top 60%',
          end: 'bottom 40%',
          scrub: 1.5
        },
        opacity: 0,
        scale: 1.02,
        ease: 'power2.out'
      }
    );
    
    gsap.fromTo(
      '.photo2',
      { opacity: 0, scale: 0.98 },
      {
        scrollTrigger: {
          trigger: '.photo-container',
          start: 'top 60%',
          end: 'bottom 40%',
          scrub: 1.5
        },
        opacity: 1,
        scale: 1,
        ease: 'power2.out'
      }
    );

    // Enhanced text animations with staggered reveals
    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: '.content-area',
        start: 'top 75%',
        end: 'top 75%',
        toggleActions: 'play none none none'
      }
    });

    tl.from('.side-label', {
      opacity: 0,
      x: -30,
      duration: 0.8,
      ease: 'power3.out'
    })
    .from('.intro-line', {
      opacity: 0,
      y: 20,
      duration: 0.6,
      ease: 'power3.out'
    }, '-=0.4')
    .from('.name-title', {
      opacity: 0,
      y: 30,
      duration: 0.8,
      ease: 'power3.out'
    }, '-=0.3')
    .from('.tag', {
      opacity: 0,
      y: 15,
      duration: 0.5,
      stagger: 0.1,
      ease: 'power3.out'
    }, '-=0.4')
    .from('.description p', {
      opacity: 0,
      y: 20,
      duration: 0.6,
      stagger: 0.2,
      ease: 'power3.out'
    }, '-=0.3');

    // Subtle parallax effect for background elements
    gsap.to('.bg-accent', {
      scrollTrigger: {
        trigger: '#about',
        start: 'top bottom',
        end: 'bottom top',
        scrub: true
      },
      y: -50,
      ease: 'none'
    });
  });
</script>

<section id="about" class="relative bg-white py-24 lg:py-32 overflow-hidden">
  <!-- Subtle background accents -->
  <div class="bg-accent absolute top-20 right-10 w-96 h-96 bg-orange-50 rounded-full blur-3xl opacity-30"></div>
  <div class="bg-accent absolute bottom-20 left-10 w-80 h-80 bg-blue-50 rounded-full blur-3xl opacity-20"></div>
  
  <!-- Side label -->
  <div class="absolute left-6 lg:left-12 top-1/2 -translate-y-1/2 hidden md:block">
    <div class="side-label -rotate-90 origin-center">
      <span class="text-xs font-medium text-gray-400 tracking-[0.2em] uppercase">
        About
      </span>
    </div>
  </div>

  <div class="mx-auto max-w-7xl px-6 lg:px-12">
    <div class="content-area grid lg:grid-cols-2 gap-16 lg:gap-20 items-center">
      
      <!-- Content Column -->
      <div class="order-2 lg:order-1 space-y-8">
        <div class="space-y-6">
          <p class="intro-line text-sm font-medium text-orange-600 tracking-wide">
            Hello, I'm
          </p>
          
          <h1 class="name-title">
            <span class="block text-4xl lg:text-5xl xl:text-6xl font-light text-gray-900 leading-[1.1]">
              Timothy
            </span>
            <span class="block text-4xl lg:text-5xl xl:text-6xl font-light text-gray-900 leading-[1.1]">
              Osorio
            </span>
          </h1>
          
          <!-- Tags with refined styling -->
          <div class="flex flex-wrap gap-2 pt-2">
            <span class="tag px-3 py-1.5 bg-gray-100 text-gray-700 text-sm font-medium rounded-full">
              Developer
            </span>
            <span class="tag px-3 py-1.5 text-sm text-gray-500 font-medium">
              Disciplined
            </span>
            <span class="tag px-3 py-1.5 text-sm text-gray-500 font-medium">
              Adaptable
            </span>
            <span class="tag px-3 py-1.5 text-sm text-gray-500 font-medium">
              Future-minded
            </span>
          </div>
        </div>

        <div class="description space-y-6 text-gray-600 leading-relaxed max-w-lg">
          <p class="text-lg">
            I'm a full stack developer with a passion for building 
            <span class="text-gray-900 font-medium">timeless, cross-platform experiences</span>.
          </p>
          
          <p>
            Whether it's websites, software, or mobile apps, I craft solutions with elegance, 
            performance, and precision. From UI to backend, cloud to device — I design systems 
            that not only work well, but <span class="text-gray-900 font-medium">feel effortless to use</span>.
          </p>
        </div>

        <!-- CTA Button -->
        <div class="pt-4">
          <button
            on:click={() => scrollToSection('#projects')}
            class="inline-flex items-center text-sm text-gray-500 group cursor-pointer hover:text-gray-700 transition-colors focus:outline-none focus:text-gray-700"
          >
            <span class="mr-2">Learn more about my work</span>
            <svg class="w-4 h-4 transition-transform group-hover:translate-x-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"></path>
            </svg>
          </button>
        </div>
      </div>

      <!-- Image Column -->
      <div class="order-1 lg:order-2 flex justify-center lg:justify-end">
        <div class="photo-container relative">
          <div class="relative w-72 h-96 lg:w-80 lg:h-[28rem]">
            <!-- Background image -->
            <div class="absolute inset-0 rounded-2xl overflow-hidden bg-gradient-to-br from-gray-100 to-gray-200">
              <img
                src="/holo.jpg"
                alt="Background texture"
                class="w-full h-full object-cover opacity-60"
              />
            </div>
            
            <!-- Profile images with improved positioning -->
            <img
              src="/prof2.JPG"
              alt="Timothy Osorio"
              class="photo2 absolute inset-0 w-full h-full object-cover rounded-2xl shadow-lg opacity-0"
            />
            <img
              src="/prof1.JPG"
              alt="Timothy Osorio"
              class="photo1 absolute inset-0 w-full h-full object-cover rounded-2xl shadow-lg"
            />
            
            <!-- Subtle overlay for better contrast -->
            <div class="absolute inset-0 rounded-2xl ring-1 ring-gray-200/50"></div>
          </div>

          <!-- Decorative elements -->
          <div class="absolute -top-4 -right-4 w-8 h-8 bg-orange-200 rounded-full opacity-60"></div>
          <div class="absolute -bottom-6 -left-6 w-12 h-12 bg-blue-100 rounded-full opacity-40"></div>
        </div>
      </div>

    </div>
  </div>
</section>