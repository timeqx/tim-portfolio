 <script>
  export let experience;
</script>
 
 <section id="experience" class="py-16 px-6 bg-white">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-3xl font-bold text-gray-900 mb-12 text-center">Experience</h2>
      <div class="space-y-8">
        {#each experience as job}
          <div class="border-l-4 border-gray-200 pl-6">
            <div class="mb-4">
              <h3 class="text-xl font-semibold text-gray-900">{job.title}</h3>
              <p class="text-gray-600">{job.company} • {job.period}</p>
            </div>
            <ul class="space-y-2">
              {#each job.responsibilities as responsibility}
                <li class="text-gray-700 flex items-start">
                  <span class="text-gray-400 mr-2">•</span>
                  {responsibility}
                </li>
              {/each}
            </ul>
          </div>
        {/each}
      </div>
    </div>
  </section>