<script lang="ts">
  import { onMount } from 'svelte';
  
  export let techStack;
  
  let mounted = false;
  let activeTab = 0;
  let hoveredSkill = null;
  
  
  
  onMount(() => {
    mounted = true;
  });
  
  function setActiveTab(index: number) {
    activeTab = index;
  }
</script>

<style>
  .tab-button {
    transition: all 0.3s cubic-bezier(0.23, 1, 0.32, 1);
  }
  
  .tab-button.active {
    transform: translateY(-2px);
  }
  
  .skill-item {
    backdrop-filter: blur(10px);
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: all 0.3s ease;
  }
  
  .skill-item:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: translateY(-2px);
  }
  
  .progress-bar {
    transition: width 1s ease-out;
    transition-delay: 0.2s;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  .fade-in {
    animation: fadeIn 0.4s ease-out;
  }
</style>

<section id="techStack" class="relative py-8 bg-gradient-to-br from-neutral-900 to-neutral-800 min-h-screen flex items-start">
  <!-- Section Label -->
  <div class="absolute left-8 top-16">
    <p class="rotate-[-90deg] text-xs font-mono text-neutral-400 tracking-[0.2em] uppercase whitespace-nowrap">
      Tech Stack
    </p>
  </div>
  
  <div class="max-w-6xl mx-auto px-6 w-full">
    <!-- Header -->
    <div class="text-center mb-12">
      <p class="text-sm font-mono text-purple-400 tracking-widest uppercase mb-4">
        Technologies & Tools
      </p>
      <h2 class="text-4xl md:text-5xl font-light text-white tracking-wide mb-6">
        What I Work With
      </h2>
    </div>
    
    <!-- Tab Navigation -->
    <div class="flex flex-wrap justify-center gap-2 mb-8">
      {#each techStack as category, index}
        <button
          class="tab-button px-4 py-3 rounded-xl font-medium text-sm transition-all duration-300 flex items-center gap-2 {activeTab === index 
            ? 'bg-gradient-to-r ' + category.gradient + ' text-white shadow-lg' 
            : 'bg-white/5 text-neutral-400 hover:bg-white/10 hover:text-white border border-white/10'}"
          on:click={() => setActiveTab(index)}
        >
          <span class="text-lg">{category.icon}</span>
          {category.category}
          <span class="text-xs opacity-70">({category.skills.length})</span>
        </button>
      {/each}
    </div>
    
    <!-- Skills Content -->
    <div class="relative">
      {#each techStack as category, categoryIndex}
        {#if activeTab === categoryIndex}
          <div class="fade-in">
            <!-- Category Header -->
            <div class="flex items-center gap-4 mb-6">
              <div class="w-3 h-3 rounded-full bg-gradient-to-r {category.gradient}"></div>
              <h3 class="text-2xl font-light text-white">{category.category}</h3>
              <div class="flex-1 h-px bg-gradient-to-r from-neutral-600 to-transparent"></div>
            </div>
            
            <!-- Skills Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
              {#each category.skills as skill, skillIndex}
                <div 
                  class="skill-item rounded-lg p-4 group"
                  style="animation-delay: {skillIndex * 0.1}s"
                >
                  <div class="flex items-center gap-3 mb-3">
                    <span class="text-xl">{skill.icon}</span>
                    <div class="flex-1">
                      <h4 class="text-white font-medium">{skill.name}</h4>
                      <div class="flex items-center gap-2 mt-1">
                        <div class="flex-1 bg-neutral-700 rounded-full h-1 overflow-hidden">
                          <div 
                            class="progress-bar h-full bg-gradient-to-r {category.gradient} rounded-full"
                            style="width: {mounted ? skill.level : 0}%"
                          ></div>
                        </div>
                        <span class="text-xs font-mono text-neutral-400">{skill.level}%</span>
                      </div>
                    </div>
                  </div>
                </div>
              {/each}
            </div>
            
            <!-- Category Stats -->
            <div class="flex justify-center">
              <div class="bg-white/5 backdrop-blur-sm rounded-xl px-6 py-3 border border-white/10">
                <div class="flex items-center gap-6 text-center">
                  <div>
                    <div class="text-xl font-light text-white">{category.skills.length}</div>
                    <div class="text-xs text-neutral-400 font-mono">Technologies</div>
                  </div>
                  <div class="w-px h-8 bg-neutral-600"></div>
                  <div>
                    <div class="text-xl font-light text-white">
                      {Math.round(category.skills.reduce((acc, skill) => acc + skill.level, 0) / category.skills.length)}%
                    </div>
                    <div class="text-xs text-neutral-400 font-mono">Avg Proficiency</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        {/if}
      {/each}
    </div>
    
    <!-- Overall Stats -->
    <div class="mt-8 pt-8 border-t border-white/10">
      <div class="grid grid-cols-4 gap-4 text-center">
        <div class="space-y-1">
          <div class="text-2xl font-light text-white">{techStack.reduce((acc, cat) => acc + cat.skills.length, 0)}</div>
          <div class="text-xs text-neutral-400 font-mono">Total Skills</div>
        </div>
        <div class="space-y-1">
          <div class="text-2xl font-light text-white">{techStack.length}</div>
          <div class="text-xs text-neutral-400 font-mono">Categories</div>
        </div>
        <div class="space-y-1">
          <div class="text-2xl font-light text-white">4+</div>
          <div class="text-xs text-neutral-400 font-mono">Years</div>
        </div>
        <div class="space-y-1">
          <div class="text-2xl font-light text-white">∞</div>
          <div class="text-xs text-neutral-400 font-mono">Learning</div>
        </div>
      </div>
    </div>
  </div>
</section>