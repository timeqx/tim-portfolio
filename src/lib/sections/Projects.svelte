<script>
  export let projects;
</script>

<section id="projects" class="bg-[#F4F3F2] relative py-16 px-6">
     <div class="absolute top-20 right-0 rotate-90">
    <p class="md:text-1xl  text-gray-500 font-semibold tracking-widest font-[plexMono] text-left text-2xl ">PROJECTS</p></div>
  <div class="relative max-w-6xl mx-auto">
  
 
    <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
      {#each projects as project}
        <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md transition-shadow">
          <h3 class="text-xl font-semibold text-gray-900 mb-3">{project.title}</h3>
          <p class="text-gray-600 mb-4">{project.description}</p>
          <div class="flex flex-wrap gap-2 mb-4">
            {#each project.tech as tech}
              <span class="px-2 py-1 bg-gray-100 text-gray-700 rounded text-sm">
                {tech}
              </span>
            {/each}
          </div>
          <div class="flex space-x-4">
            <a href={project.github} target="_blank" rel="noopener noreferrer" class="text-gray-600 hover:text-gray-900 transition-colors">
              GitHub
            </a>
       
            <a href={project.demo} target="_blank" rel="noopener noreferrer" class="text-gray-600 hover:text-gray-900 transition-colors">
              Live Demo
            </a>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>
