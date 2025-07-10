<script>
  export let projects;
</script>

<section id="projects" class="py-16 px-6">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-3xl font-bold text-gray-900 mb-12 text-center">Projects</h2>
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
