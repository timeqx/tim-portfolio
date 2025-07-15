<script lang="ts">
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

  export let profile;

  let sectionRef: HTMLElement | null;
let titleRef: HTMLElement | null;
let descriptionRef: HTMLElement | null;
let contactLinksRef: HTMLElement | null;
let buttonRef: HTMLButtonElement | null;

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    // Timeline for contact section animations
    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: sectionRef,
        start: 'top 80%',
        end: 'bottom 20%',
        toggleActions: 'play none none none', 
      }
    });

    // Animate title
    tl.fromTo(titleRef, 
      { opacity: 0, y: 50 },
      { opacity: 1, y: 0, duration: 1, ease: 'power2.out' }
    );

    // Animate description
    tl.fromTo(descriptionRef,
      { opacity: 0, y: 30 },
      { opacity: 1, y: 0, duration: 0.8, ease: 'power2.out' },
      '-=0.5'
    );

    // Animate contact links
    if(contactLinksRef){
    tl.fromTo(contactLinksRef.children,
      { opacity: 0, y: 20, scale: 0.9 },
      { opacity: 1, y: 0, scale: 1, duration: 0.6, stagger: 0.1, ease: 'back.out(1.7)' },
      '-=0.3'
    );}

    // Animate button
    tl.fromTo(buttonRef,
      { opacity: 0, y: 30 },
      { opacity: 1, y: 0, duration: 0.6, ease: 'power2.out' },
      '-=0.2'
    );

    // Hover animations for contact links
    if(contactLinksRef){
      
    contactLinksRef.children.forEach((link: HTMLElement) => {
      link.addEventListener('mouseenter', () => {
        gsap.to(link, { scale: 1.05, duration: 0.3, ease: 'power2.out' });
      });
      
      link.addEventListener('mouseleave', () => {
        gsap.to(link, { scale: 1, duration: 0.3, ease: 'power2.out' });
      });
    });
  }

    if(buttonRef){
    buttonRef.addEventListener('mouseenter', () => {
      gsap.to(buttonRef, { scale: 1.05, duration: 0.3, ease: 'power2.out' });
    });
    }
   if(buttonRef){
    buttonRef.addEventListener('mouseleave', () => {
      gsap.to(buttonRef, { scale: 1, duration: 0.3, ease: 'power2.out' });
    });}
  });
</script>

<section 
  bind:this={sectionRef}
  id="contact" 
  class="relative bg-black text-white py-10 px-6 overflow-hidden"
>
  <!-- Animated background elements -->
  <div class="absolute inset-0 opacity-10">
    <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-gradient-to-r from-[#8F4816] to-[#FAC050ff] rounded-full blur-3xl"></div>
    <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-gradient-to-r from-[#B36673ff] to-[#9471CBff] rounded-full blur-3xl"></div>
  </div>

  <div class="relative max-w-4xl mx-auto text-center">
    <!-- Title -->
    <p 
      bind:this={titleRef}
      class="text-lg md:text-3xl font-bold mb-6 bg-gradient-to-r from-white to-gray-300 bg-clip-text text-transparent"
    >
      Let's Connect
  </p>

    <!-- Description -->
    <p 
      bind:this={descriptionRef}
      class="text-md md:text-lg text-gray-300 mb-8 max-w-2xl mx-auto leading-relaxed"
    >
      Ready to bring your ideas to life? I'm here to help turn your vision into reality.
    </p>

    <!-- Contact Links -->
    <div bind:this={contactLinksRef} class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-16">
      <!-- Email -->
      <a 
        href="mailto:{profile.email}"
        class="group bg-gray-900/50 backdrop-blur-sm border border-gray-700 rounded-2xl p-6 hover:border-red-500 transition-all duration-300"
      >
        <div class="flex flex-col items-center space-y-3">
          <div class="w-12 h-12 bg-gradient-to-r from-red-500 to-red-600 rounded-full flex items-center justify-center">
           <svg class="w-6 h-6 text-white" viewBox="0 0 24 24" fill="currentColor">
  <path d="M24 5.457v13.909c0 .904-.732 1.636-1.636 1.636h-3.819V11.73L12 16.64l-6.545-4.91v9.273H1.636A1.636 1.636 0 0 1 0 19.366V5.457c0-2.023 2.309-3.178 3.927-1.964L5.455 4.64 12 9.548l6.545-4.91 1.528-1.145C21.69 2.28 24 3.434 24 5.457z"/>
</svg>
          </div>
          <span class="text-gray-300 group-hover:text-white transition-colors text-sm font-medium">Email</span>
          <span class="text-xs text-gray-500 break-all">{profile.email}</span>
        </div>
      </a>

      <!-- Phone -->
      <div
       
        class="group bg-gray-900/50 backdrop-blur-sm border border-gray-700 rounded-2xl p-6 hover:border-green-500 transition-all duration-300"
      >
        <div class="flex flex-col items-center space-y-3">
          <div class="w-12 h-12 bg-gradient-to-r from-green-500 to-green-600 rounded-full flex items-center justify-center">
            <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/>
            </svg>
          </div>
          <span class="text-gray-300 group-hover:text-white transition-colors text-sm font-medium">Phone</span>
          <span class="text-xs text-gray-500">{profile.phone}</span>
        </div>
      </div>

      <!-- GitHub -->
      <a 
        href="https://github.com/{profile.github}"
        target="_blank"
        rel="noopener noreferrer"
        class="group bg-gray-900/50 backdrop-blur-sm border border-gray-700 rounded-2xl p-6 hover:border-purple-500 transition-all duration-300"
      >
        <div class="flex flex-col items-center space-y-3">
          <div class="w-12 h-12 bg-gradient-to-r from-purple-500 to-purple-600 rounded-full flex items-center justify-center">
            <svg class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"/>
            </svg>
          </div>
          <span class="text-gray-300 group-hover:text-white transition-colors text-sm font-medium">GitHub</span>
          <span class="text-xs text-gray-500">@{profile.github}</span>
        </div>
      </a>

      <!-- LinkedIn -->
      <a 
        href="https://linkedin.com/in/{profile.linkedin}"
        target="_blank"
        rel="noopener noreferrer"
        class="group bg-gray-900/50 backdrop-blur-sm border border-gray-700 rounded-2xl p-6 hover:border-blue-400 transition-all duration-300"
      >
        <div class="flex flex-col items-center space-y-3">
          <div class="w-12 h-12 bg-gradient-to-r from-blue-400 to-blue-500 rounded-full flex items-center justify-center">
            <svg class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M16.338 16.338H13.67V12.16c0-.995-.017-2.277-1.387-2.277-1.39 0-1.601 1.086-1.601 2.207v4.248H8.014v-8.59h2.559v1.174h.037c.356-.675 1.227-1.387 2.526-1.387 2.703 0 3.203 1.778 3.203 4.092v4.711zM5.005 6.575a1.548 1.548 0 11-.003-3.096 1.548 1.548 0 01.003 3.096zm-1.337 9.763H6.34v-8.59H3.667v8.59zM17.668 1H2.328C1.595 1 1 1.581 1 2.298v15.403C1 18.418 1.595 19 2.328 19h15.34c.734 0 1.332-.582 1.332-1.299V2.298C19 1.581 18.402 1 17.668 1z" clip-rule="evenodd"/>
            </svg>
          </div>
          <span class="text-gray-300 group-hover:text-white transition-colors text-sm font-medium">LinkedIn</span>
          <span class="text-xs text-gray-500">@{profile.linkedin}</span>
        </div>
      </a>
    </div>

    <!-- CTA Button -->
    <button 
      bind:this={buttonRef}
      on:click={() => window.location.href = `mailto:${profile.email}`}
      class="group relative bg-gradient-to-r from-[#9471CBff] to-[#5A30B6ff] text-white px-8 py-3 rounded-full font-medium text-md transition-all duration-300 hover:shadow-2xl hover:shadow-purple-500/50"
    >
      <span class="relative z-10 flex items-center space-x-2">
        <span>Start a Conversation</span>
        <svg class="w-5 h-5 group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6"/>
        </svg>
      </span>
      <div class="absolute inset-0 bg-gradient-to-r from-[#9471CBff] to-[#5A30B6ff] rounded-full opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
    </button>
  </div>
</section>