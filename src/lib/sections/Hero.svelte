<script>
  import { onMount } from 'svelte';
  
  export let profile;
  
  let mounted = false;
  
  onMount(() => {
    mounted = true;
  });
</script>

<style>
  @keyframes subtle-float {
    0%, 100% { transform: translateY(0px) rotate(0deg); }
    50% { transform: translateY(-8px) rotate(1deg); }
  }
  
  @keyframes gentle-pulse {
    0%, 100% { opacity: 0.4; transform: scale(1); }
    50% { opacity: 0.7; transform: scale(1.05); }
  }
  
  @keyframes text-reveal {
    from { 
      opacity: 0; 
      transform: translateY(30px);
      filter: blur(10px);
    }
    to { 
      opacity: 1; 
      transform: translateY(0px);
      filter: blur(0px);
    }
  }
  
  @keyframes fade-up {
    from { 
      opacity: 0; 
      transform: translateY(40px);
    }
    to { 
      opacity: 1; 
      transform: translateY(0px);
    }
  }
  
  .hero-text {
    animation: text-reveal 1.2s ease-out 0.5s both;
  }
  
  .hero-subtitle {
    animation: text-reveal 1.2s ease-out 0.8s both;
  }
  
  .floating-accent {
    animation: subtle-float 6s ease-in-out infinite;
  }
  
  .ambient-glow {
    animation: gentle-pulse 8s ease-in-out infinite;
  }
  
  .text-gradient {
    background: linear-gradient(135deg, #e5e5e5 0%, #a3a3a3 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  
  .accent-gradient {
    background: linear-gradient(135deg, #9471cb 0%, #b36673 50%, #fac050 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }
</style>

<!-- Hero Section -->
<section class="relative min-h-screen flex items-center justify-center bg-[#131010] overflow-hidden">
  <!-- Ambient Background -->
  <div class="absolute inset-0">
    <!-- Subtle gradient orbs -->
    <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-gradient-to-br from-[#8F4816]/10 to-[#FAC050]/5 rounded-full blur-3xl ambient-glow"></div>
    <div class="absolute bottom-1/3 right-1/4 w-80 h-80 bg-gradient-to-bl from-[#9471CB]/8 to-[#B36673]/5 rounded-full blur-3xl ambient-glow" style="animation-delay: 2s;"></div>
    
    <!-- Floating accent elements -->
    <div class="absolute top-20 right-20 w-2 h-2 bg-[#FAC050]/60 rounded-full floating-accent"></div>
    <div class="absolute bottom-32 left-16 w-1 h-1 bg-[#9471CB]/40 rounded-full floating-accent" style="animation-delay: 3s;"></div>
  </div>
  
  <!-- Main Content -->
  <div class="relative z-10 max-w-4xl mx-auto px-6 text-center">
    <!-- Name -->
    <h1 class="hero-text mb-6 text-5xl sm:text-6xl md:text-7xl lg:text-8xl font-light tracking-wider text-gradient font-mono">
      {profile?.name || 'Timothy Osorio'}
    </h1>
    
    <!-- Tagline -->
    <p class="hero-subtitle text-xl sm:text-2xl md:text-3xl font-light text-neutral-400 max-w-3xl mx-auto leading-relaxed">
      Full Stack Developer crafting
      <span class="accent-gradient font-medium">elegant solutions</span>
      from concept to deployment
    </p>
    
    <!-- Minimal CTA -->
    <div class="mt-12 opacity-0 animate-[fade-up_1s_ease-out_1.2s_both]">
      <div class="inline-flex items-center space-x-2 text-neutral-500 text-sm tracking-widest">
        <span>SCROLL TO EXPLORE</span>
        <div class="w-4 h-4 border border-neutral-500 border-t-0 border-l-0 rotate-45 animate-bounce"></div>
      </div>
    </div>
  </div>
</section>