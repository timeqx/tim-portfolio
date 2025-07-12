<script>
  import { onMount } from 'svelte';
  
  // Array of cube configurations with original positions
  const cubes = [
    { 
      size: 'h-24 w-24', 
      shadow: 'shadow-[0_10px_15px_#8F4816ff]', 
      hoverShadow: 'group-hover:shadow-[5px_-5px_25px_#FAC050ff]',
      position: '-top-10 left-10',
      orbitRadius: 30,
      orbitSpeed: 30
    },
    { 
      size: 'h-12 w-12', 
      shadow: 'shadow-[0_-5px_15px_#FAC050ff]', 
      hoverShadow: 'group-hover:shadow-[5px_5px_20px_#8F4816ff]',
      position: 'top-40 left-30',
      orbitRadius: 25,
      orbitSpeed: 29
    },
    { 
      size: 'h-20 w-20', 
      shadow: 'shadow-[0_-5px_15px_#9471CBff]', 
      hoverShadow: 'group-hover:shadow-[5px_5px_20px_#5A30B6ff]',
      position: 'top-90 right-140',
      orbitRadius: 35,
      orbitSpeed: 28
    },
    { 
      size: 'h-28 w-28', 
      shadow: 'shadow-[0_12px_20px_#8b5cf6]', 
      hoverShadow: 'group-hover:shadow-[6px_6px_35px_#d8b4fe]',
      position: 'top-150 right-40',
      orbitRadius: 40,
      orbitSpeed: 26
    },
    { 
      size: 'h-8 w-8', 
      shadow: 'shadow-[5px_0_10px_#B36673ff]', 
      hoverShadow: 'group-hover:shadow-[-2px_-2px_15px_#9471CBff]',
      position: 'top-30 right-170',
      orbitRadius: 20,
      orbitSpeed: 32
    },
    { 
      size: 'h-16 w-16', 
      shadow: 'shadow-[10px_0_15px_#6b21a8]', 
      hoverShadow: 'group-hover:shadow-[0_-10px_30px_#c084fc]',
      position: 'top-100 right-60',
      orbitRadius: 30,
      orbitSpeed: 40
    }
  ];
</script>

<style>
 

  @keyframes orbitRoll {
     from  {
    transform: translate3d(20rem, 0rem, 20rem);
  }
  to  {
    transform: translate3d(-20rem, -2rem, 20rem);
  }

}
  .rolling-element {
    
  animation: orbitRoll 20s linear infinite;
  transform-style: preserve-3d;
}
  
  .orbit-container {
    transform-style: preserve-3d;
    perspective: 1000px;
  }
  
  .cube {
    transform-style: preserve-3d;
    position: relative;
  }
  
  .cube::before {
    content: '';
    position: absolute;
    top: -3px;
    left: -3px;
    width: 100%;
    height: 100%;
    background: inherit;
    border-radius: inherit;
    transform: translateZ(-6px) scale(0.9);
    opacity: 0.6;
    box-shadow: inherit;
  }
  
  .cube::after {
    content: '';
    position: absolute;
    top: -2px;
    right: -4px;
    width: 100%;
    height: 100%;
    background: inherit;
    border-radius: inherit;
    transform: rotateY(90deg) translateZ(-3px) scale(0.95);
    opacity: 0.4;
    box-shadow: inherit;
  }
  
  .orbiting-cube {
    animation: orbit45 var(--orbit-speed) linear infinite;
  }
  
  .orbit-anchor {
    transform-style: preserve-3d;
  }
</style>

<div class=" absolute inset-0  right-2 z-20 orbit-container rolling-element ">
  {#each cubes as cube, index}
    <div class="group absolute {cube.position} z-0 orbit-anchor">
      <div 
        class="orbiting-cube"
        style="--orbit-radius: {cube.orbitRadius}px; --orbit-speed: {cube.orbitSpeed}s;"
      >
        <div
          class="cube {cube.size} rounded-lg bg-[#181616] {cube.shadow} backdrop-blur-md transition-all duration-[3s] ease-out {cube.hoverShadow}"
        ></div>
      </div>
    </div>
  {/each}
</div>