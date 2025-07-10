<!-- src/routes/+page.svelte -->
<script>
  import { onMount } from 'svelte';
  
  let mounted = false;
  
  onMount(() => {
    mounted = true;
  });

  // Portfolio data - replace with your actual information
  

  

 

 

 

 

  let activeSection = 'about';
  
  function scrollToSection(sectionId) {
    activeSection = sectionId;
    document.getElementById(sectionId)?.scrollIntoView({ behavior: 'smooth' });
  }
</script>

<svelte:head>
  <title>{profile.name} - Portfolio</title>
  <meta name="description" content="{profile.name} - {profile.title} Portfolio" />
</svelte:head>

<div class="min-h-screen bg-gray-50">
  <!-- Navigation -->
  <nav class="fixed top-0 w-full bg-white/80 backdrop-blur-sm border-b border-gray-200 z-50">
    <div class="max-w-6xl mx-auto px-6 py-4">
      <div class="flex items-center justify-between">
        <div class="font-semibold text-xl text-gray-900">{profile.name}</div>
        <div class="hidden md:flex space-x-8">
          <button 
            on:click={() => scrollToSection('about')}
            class="text-gray-600 hover:text-gray-900 transition-colors"
            class:text-gray-900={activeSection === 'about'}
          >
            About
          </button>
          <button 
            on:click={() => scrollToSection('experience')}
            class="text-gray-600 hover:text-gray-900 transition-colors"
            class:text-gray-900={activeSection === 'experience'}
          >
            Experience
          </button>
          <button 
            on:click={() => scrollToSection('projects')}
            class="text-gray-600 hover:text-gray-900 transition-colors"
            class:text-gray-900={activeSection === 'projects'}
          >
            Projects
          </button>
          <button 
            on:click={() => scrollToSection('education')}
            class="text-gray-600 hover:text-gray-900 transition-colors"
            class:text-gray-900={activeSection === 'education'}
          >
            Education
          </button>
          <button 
            on:click={() => scrollToSection('contact')}
            class="text-gray-600 hover:text-gray-900 transition-colors"
            class:text-gray-900={activeSection === 'contact'}
          >
            Contact
          </button>
        </div>
      </div>
    </div>
  </nav>

  <!-- Hero Section -->
  <section id="about" class="pt-24 pb-16 px-6">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-16">
        <h1 class="text-5xl md:text-6xl font-bold text-gray-900 mb-6">
          {profile.name}
        </h1>
        <p class="text-xl md:text-2xl text-gray-600 mb-8">
          {profile.title}
        </p>
        <p class="text-lg text-gray-700 max-w-2xl mx-auto leading-relaxed">
          {profile.bio}
        </p>
      </div>

      <!-- Moving Gallery Showcase -->
      <div class="mb-16">
        <div class="overflow-hidden rounded-2xl bg-gray-50 outline outline-gray-950/5 flex h-96 items-center justify-center">
          <div class="w-full h-full shrink-0 scale-50 sm:scale-75 lg:scale-100">
            <div class="relative top-1/4 right-1/2 grid w-full h-full origin-top-left grid-cols-4 gap-4 transform-3d gallery-perspective">
              <!-- Column 1 -->
              <div class="flex flex-col gap-4 gallery-column" style="animation: gallery-float-1 20s infinite linear;">
                <div class="aspect-970/580 ring ring-gray-950/5 bg-white rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">E-commerce Platform</h3>
                    <p class="text-sm text-gray-600">React • Node.js • PostgreSQL</p>
                  </div>
                </div>
                <div class="aspect-971/582 ring ring-gray-950/5 bg-white rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Task Manager</h3>
                    <p class="text-sm text-gray-600">SvelteKit • Socket.io</p>
                  </div>
                </div>
                <div class="aspect-971/820 ring ring-gray-950/5 bg-white rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Weather Dashboard</h3>
                    <p class="text-sm text-gray-600">Vue.js • Chart.js</p>
                  </div>
                </div>
                <div class="aspect-970/508 ring ring-gray-950/5 bg-white rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Portfolio Site</h3>
                    <p class="text-sm text-gray-600">SvelteKit • Tailwind</p>
                  </div>
                </div>
              </div>

              <!-- Column 2 -->
              <div class="flex flex-col gap-4 gallery-column" style="animation: gallery-float-2 20s infinite linear;">
                <div class="aspect-970/436 ring ring-gray-950/5 bg-gradient-to-br from-blue-50 to-indigo-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">API Gateway</h3>
                    <p class="text-sm text-gray-600">Node.js • Express</p>
                  </div>
                </div>
                <div class="aspect-970/700 ring ring-gray-950/5 bg-gradient-to-br from-green-50 to-emerald-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Chat Application</h3>
                    <p class="text-sm text-gray-600">React • WebSockets</p>
                  </div>
                </div>
                <div class="aspect-971/879 ring ring-gray-950/5 bg-gradient-to-br from-purple-50 to-violet-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Data Visualization</h3>
                    <p class="text-sm text-gray-600">D3.js • Python</p>
                  </div>
                </div>
                <div class="aspect-970/557 ring ring-gray-950/5 bg-gradient-to-br from-orange-50 to-red-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Mobile App</h3>
                    <p class="text-sm text-gray-600">React Native</p>
                  </div>
                </div>
                <div class="aspect-970/763 ring ring-gray-950/5 bg-gradient-to-br from-teal-50 to-cyan-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Cloud Functions</h3>
                    <p class="text-sm text-gray-600">AWS Lambda</p>
                  </div>
                </div>
                <div class="aspect-970/922 ring ring-gray-950/5 bg-gradient-to-br from-pink-50 to-rose-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Authentication</h3>
                    <p class="text-sm text-gray-600">JWT • OAuth</p>
                  </div>
                </div>
              </div>

              <!-- Column 3 -->
              <div class="flex flex-col gap-4 gallery-column" style="animation: gallery-float-3 20s infinite linear;">
                <div class="aspect-970/580 ring ring-gray-950/5 bg-gradient-to-br from-slate-50 to-gray-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">CMS System</h3>
                    <p class="text-sm text-gray-600">Headless CMS</p>
                  </div>
                </div>
                <div class="aspect-971/395 ring ring-gray-950/5 bg-gradient-to-br from-amber-50 to-yellow-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Payment Gateway</h3>
                    <p class="text-sm text-gray-600">Stripe • PayPal</p>
                  </div>
                </div>
                <div class="aspect-971/349 ring ring-gray-950/5 bg-gradient-to-br from-lime-50 to-green-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Analytics Dashboard</h3>
                    <p class="text-sm text-gray-600">Charts • Metrics</p>
                  </div>
                </div>
                <div class="aspect-970/975 ring ring-gray-950/5 bg-gradient-to-br from-indigo-50 to-blue-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">AI Integration</h3>
                    <p class="text-sm text-gray-600">OpenAI • TensorFlow</p>
                  </div>
                </div>
                <div class="aspect-970/381 ring ring-gray-950/5 bg-gradient-to-br from-rose-50 to-pink-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Microservices</h3>
                    <p class="text-sm text-gray-600">Docker • Kubernetes</p>
                  </div>
                </div>
                <div class="aspect-970/782 ring ring-gray-950/5 bg-gradient-to-br from-cyan-50 to-teal-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">GraphQL API</h3>
                    <p class="text-sm text-gray-600">Apollo • Prisma</p>
                  </div>
                </div>
                <div class="aspect-970/426 ring ring-gray-950/5 bg-gradient-to-br from-violet-50 to-purple-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Testing Suite</h3>
                    <p class="text-sm text-gray-600">Jest • Cypress</p>
                  </div>
                </div>
              </div>

              <!-- Column 4 -->
              <div class="flex flex-col gap-4 gallery-column" style="animation: gallery-float-4 20s infinite linear;">
                <div class="aspect-970/600 ring ring-gray-950/5 bg-gradient-to-br from-emerald-50 to-teal-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">DevOps Pipeline</h3>
                    <p class="text-sm text-gray-600">CI/CD • GitHub Actions</p>
                  </div>
                </div>
                <div class="aspect-972/854 ring ring-gray-950/5 bg-gradient-to-br from-orange-50 to-amber-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Blockchain DApp</h3>
                    <p class="text-sm text-gray-600">Ethereum • Solidity</p>
                  </div>
                </div>
                <div class="aspect-971/725 ring ring-gray-950/5 bg-gradient-to-br from-red-50 to-pink-100 rounded-lg p-6 flex items-center justify-center">
                  <div class="text-center">
                    <h3 class="font-semibold text-gray-900 mb-2">Machine Learning</h3>
                    <p class="text-sm text-gray-600">Python • scikit-learn</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Tech Stack -->
      <div class="mb-16">
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
    </div>
  </section>

  <!-- Experience Section -->
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

  <!-- Projects Section -->
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
              <a 
                href={project.github} 
                target="_blank" 
                rel="noopener noreferrer"
                class="text-gray-600 hover:text-gray-900 transition-colors"
              >
                GitHub
              </a>
              <a 
                href={project.demo} 
                target="_blank" 
                rel="noopener noreferrer"
                class="text-gray-600 hover:text-gray-900 transition-colors"
              >
                Live Demo
              </a>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Education & Certifications -->
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

  <!-- Contact Section -->
  <section id="contact" class="py-16 px-6">
    <div class="max-w-6xl mx-auto text-center">
      <h2 class="text-3xl font-bold text-gray-900 mb-8">Get In Touch</h2>
      <p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
        I'm always open to discussing new opportunities, interesting projects, or just having a chat about technology.
      </p>
      
      <div class="flex flex-wrap justify-center gap-6 mb-8">
        <a 
          href="mailto:{profile.email}"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>✉️</span>
          <span>{profile.email}</span>
        </a>
        <a 
          href="tel:{profile.phone}"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>📱</span>
          <span>{profile.phone}</span>
        </a>
        <a 
          href="https://github.com/{profile.github}"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>🐙</span>
          <span>GitHub</span>
        </a>
        <a 
          href="https://linkedin.com/in/{profile.linkedin}"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center space-x-2 text-gray-600 hover:text-gray-900 transition-colors"
        >
          <span>💼</span>
          <span>LinkedIn</span>
        </a>
      </div>

      <button 
        on:click={() => window.location.href = `mailto:${profile.email}`}
        class="bg-gray-900 text-white px-8 py-3 rounded-lg hover:bg-gray-800 transition-colors"
      >
        Send Message
      </button>
    </div>
  </section>

  <!-- Footer -->
  <footer class="bg-gray-900 text-white py-8 px-6">
    <div class="max-w-6xl mx-auto text-center">
      <p class="text-gray-400">
        © 2024 {profile.name}. Built with SvelteKit & Tailwind CSS.
      </p>
    </div>
  </footer>
</div>

<style>
  :global(html) {
    scroll-behavior: smooth;
  }
  
  .gallery-perspective {
    transform: rotateX(55deg) rotateY(0deg) rotateZ(-45deg);
    transform-style: preserve-3d;
  }
  
  .gallery-column {
    transform-style: preserve-3d;
  }
  
  @keyframes gallery-float-1 {
    0% { transform: translateY(0px); }
    100% { transform: translateY(-100px); }
  }
  
  @keyframes gallery-float-2 {
    0% { transform: translateY(0px); }
    100% { transform: translateY(-120px); }
  }
  
  @keyframes gallery-float-3 {
    0% { transform: translateY(0px); }
    100% { transform: translateY(-80px); }
  }
  
  @keyframes gallery-float-4 {
    0% { transform: translateY(0px); }
    100% { transform: translateY(-140px); }
  }
  
  .aspect-970\/580 { aspect-ratio: 970/580; }
  .aspect-971\/582 { aspect-ratio: 971/582; }
  .aspect-971\/820 { aspect-ratio: 971/820; }
  .aspect-970\/508 { aspect-ratio: 970/508; }
  .aspect-970\/436 { aspect-ratio: 970/436; }
  .aspect-970\/700 { aspect-ratio: 970/700; }
  .aspect-971\/879 { aspect-ratio: 971/879; }
  .aspect-970\/557 { aspect-ratio: 970/557; }
  .aspect-970\/763 { aspect-ratio: 970/763; }
  .aspect-970\/922 { aspect-ratio: 970/922; }
  .aspect-971\/395 { aspect-ratio: 971/395; }
  .aspect-971\/349 { aspect-ratio: 971/349; }
  .aspect-970\/975 { aspect-ratio: 970/975; }
  .aspect-970\/381 { aspect-ratio: 970/381; }
  .aspect-970\/782 { aspect-ratio: 970/782; }
  .aspect-970\/426 { aspect-ratio: 970/426; }
  .aspect-970\/600 { aspect-ratio: 970/600; }
  .aspect-972\/854 { aspect-ratio: 972/854; }
  .aspect-971\/725 { aspect-ratio: 971/725; }
  
  .transform-3d {
    transform-style: preserve-3d;
  }
</style>