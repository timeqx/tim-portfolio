<script>
  export let techStack;
</script>

<section class="mb-16 px-6">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-3xl font-bold text-gray-900 mb-8 text-center">Tech Stack</h2>
    <div class="grid md:grid-cols-3 gap-8">
      {#each techStack as category}
        <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200">
          <h3 class="text-xl font-semibold text-gray-900 mb-4">{category.category}</h3>
          <div class="flex flex-wrap gap-2">
            {#each category.skills as skill}
              <span class="px-3 py-1 bg-gray-100 text-gray-700 rounded-full text-sm">
                {skill}
              </span>
            {/each}
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>
