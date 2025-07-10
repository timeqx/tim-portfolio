<script lang="ts">
  export let education: {
    degree: string;
    institution: string;
    year: string;
    gpa: string;
  }[];

  export let certifications: {
    name: string;
    issuer: string;
    year: string;
    id: string;
  }[];
</script>

<section id="education" class="py-16 px-6 bg-white">
  <div class="max-w-6xl mx-auto">
    <div class="grid md:grid-cols-2 gap-12">
      <!-- Education -->
      <div>
        <h2 class="text-3xl font-bold text-gray-900 mb-8">Education</h2>
        <div class="space-y-6">
          {#each education as edu}
            <div class="border-l-4 border-gray-200 pl-6">
              <h3 class="text-xl font-semibold text-gray-900">{edu.degree}</h3>
              <p class="text-gray-600">{edu.institution}</p>
              <p class="text-gray-500">{edu.year} • {edu.gpa}</p>
            </div>
          {/each}
        </div>
      </div>

      <!-- Certifications -->
      <div>
        <h2 class="text-3xl font-bold text-gray-900 mb-8">Certifications</h2>
        <div class="space-y-6">
          {#each certifications as cert}
            <div class="border-l-4 border-gray-200 pl-6">
              <h3 class="text-xl font-semibold text-gray-900">{cert.name}</h3>
              <p class="text-gray-600">{cert.issuer}</p>
              <p class="text-gray-500">{cert.year} • {cert.id}</p>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>
