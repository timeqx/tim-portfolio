<script>
  import { onMount } from 'svelte';
  
  // Minimal cube configurations - fewer cubes, cleaner arrangement
  const cubes = [
    { 
      size: 'h-16 w-16', 
      shadow: 'shadow-[0_8px_32px_rgba(143,72,22,0.3)]', 
      hoverShadow: 'hover:shadow-[0_12px_40px_rgba(250,192,80,0.4)]',
      position: 'top-[15%] left-[10%]',
      delay: '0s'
    },
    { 
      size: 'h-12 w-12', 
      shadow: 'shadow-[0_6px_24px_rgba(148,113,203,0.25)]', 
      hoverShadow: 'hover:shadow-[0_10px_32px_rgba(90,48,182,0.35)]',
      position: 'top-[60%] left-[15%]',
      delay: '2s'
    },
    { 
      size: 'h-20 w-20', 
      shadow: 'shadow-[0_10px_36px_rgba(179,102,115,0.3)]', 
      hoverShadow: 'hover:shadow-[0_15px_48px_rgba(148,113,203,0.4)]',
      position: 'top-[25%] right-[12%]',
      delay: '4s'
    },
    { 
      size: 'h-14 w-14', 
      shadow: 'shadow-[0_7px_28px_rgba(107,33,168,0.25)]', 
      hoverShadow: 'hover:shadow-[0_12px_36px_rgba(192,132,252,0.35)]',
      position: 'top-[70%] right-[8%]',
      delay: '6s'
    },
    { 
      size: 'h-10 w-10', 
      shadow: 'shadow-[0_5px_20px_rgba(250,193,21,0.2)]', 
      hoverShadow: 'hover:shadow-[0_8px_28px_rgba(250,192,80,0.3)]',
      position: 'top-[45%] left-[50%]',
      delay: '8s'
    }
  ];

  let mounted = false;
  
  onMount(() => {
    mounted = true;
  });
</script>

<style>
  @keyframes float {
    0%, 100% {
      transform: translate3d(0, 0, 0) rotateX(0deg) rotateY(0deg);
    }
    25% {
      transform: translate3d(10px, -15px, 5px) rotateX(5deg) rotateY(10deg);
    }
    50% {
      transform: translate3d(-5px, -25px, 10px) rotateX(-3deg) rotateY(-5deg);
    }
    75% {
      transform: translate3d(-15px, -10px, 5px) rotateX(2deg) rotateY(-8deg);
    }
  }

  @keyframes fadeInFloat {
    0% {
      opacity: 0;
      transform: translate3d(0, 50px, -20px) scale(0.8);
    }
    100% {
      opacity: 1;
      transform: translate3d(0, 0, 0) scale(1);
    }
  }

  @keyframes subtleGlow {
    0%, 100% {
      filter: brightness(1);
    }
    50% {
      filter: brightness(1.1);
    }
  }

  .cube {
    transform-style: preserve-3d;
    position: relative;
    animation: float 8s ease-in-out infinite;
    will-change: transform;
  }

  .cube::before {
    content: '';
    position: absolute;
    top: -2px;
    left: -2px;
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, rgba(19,16,16,0.9) 0%, rgba(25,20,20,0.8) 100%);
    border-radius: inherit;
    transform: translateZ(-4px) scale(0.95);
    opacity: 0.7;
    border: 1px solid rgba(255,255,255,0.05);
  }

  .cube::after {
    content: '';
    position: absolute;
    top: -1px;
    right: -3px;
    width: 100%;
    height: 100%;
    background: linear-gradient(45deg, rgba(19,16,16,0.8) 0%, rgba(30,25,25,0.7) 100%);
    border-radius: inherit;
    transform: rotateY(90deg) translateZ(-2px) scale(0.98);
    opacity: 0.5;
    border: 1px solid rgba(255,255,255,0.03);
  }

  .cube-container {
    animation: fadeInFloat 2s ease-out forwards;
    animation-delay: var(--delay);
    opacity: 0;
  }

  .cube-container:nth-child(odd) .cube {
    animation-direction: reverse;
  }

  .cube-container:hover .cube {
    animation-duration: 4s;
    filter: brightness(1.15);
  }

  .floating-field {
    transform-style: preserve-3d;
    perspective: 1200px;
  }

  .backdrop-element {
    background: rgba(19,16,16,0.92);
    backdrop-filter: blur(1px);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 8px;
    transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
  }

  @media (max-width: 768px) {
    .cube-container {
      transform: scale(0.8);
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .cube, .cube-container {
      animation: none;
    }
    .cube {
      transform: none;
    }
  }
</style>

<!-- Floating Cube Field Background -->
<div class="absolute inset-0 z-10 floating-field pointer-events-none overflow-hidden">
  {#if mounted}
    {#each cubes as cube, index}
      <div 
        class="cube-container absolute {cube.position} group"
        style="--delay: {cube.delay}"
      >
        <div
          class="cube {cube.size} backdrop-element {cube.shadow} transition-shadow duration-500 {cube.hoverShadow}"
          style="animation-delay: {parseFloat(cube.delay) + index * 0.5}s"
        ></div>
      </div>
    {/each}
  {/if}

  <!-- Subtle ambient particles -->
  <div class="absolute top-[20%] left-[25%] w-1 h-1 bg-gradient-to-r from-[#9471CB] to-transparent rounded-full opacity-60 animate-pulse" style="animation-delay: 3s;"></div>
  <div class="absolute top-[80%] right-[30%] w-1 h-1 bg-gradient-to-r from-[#FAC050] to-transparent rounded-full opacity-40 animate-pulse" style="animation-delay: 7s;"></div>
  <div class="absolute top-[35%] right-[60%] w-0.5 h-0.5 bg-gradient-to-r from-[#B36673] to-transparent rounded-full opacity-50 animate-pulse" style="animation-delay: 12s;"></div>
</div>