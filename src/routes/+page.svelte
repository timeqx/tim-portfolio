<!-- src/routes/+page.svelte -->
<script lang="ts">
  import Hero from '$lib/sections/Hero.svelte';
 import Iam from '$lib/sections/Iam.svelte';
  import TechStack from '$lib/sections/TechStack.svelte';
  import Gallery from '$lib/sections/Gallery.svelte';
  import Projects from '$lib/sections/Projects.svelte';
  import EducationCerts from '$lib/sections/EducationCerts.svelte';
  import Contact from '$lib/sections/Contact.svelte';
  import Footer from '$lib/sections/Footer.svelte';
  import { onMount } from 'svelte';
  

  let mounted = false;
  onMount(() => { mounted = true; });

  import {profile} from '$lib/data/profile';
  import {techStack} from '$lib/data/techStack';
  import {projects} from '$lib/data/projects';
  import {education} from '$lib/data/education';
  import {certifications} from '$lib/data/certifications';
  import {experience} from '$lib/data/experience';

  let activeSection = 'about';
  function scrollToSection(sectionId: string) {
  activeSection = sectionId;
  document.getElementById(sectionId)?.scrollIntoView({ behavior: 'smooth' });
}
</script>

<svelte:head>
  <title>timeqx dev</title>
  <meta name="description" content="{profile.name} - {profile.title} Portfolio" />
</svelte:head>

<div class="min-h-screen">
  <!-- Navigation -->
  <nav class=" top-0 w-full absolute  bg-transparent  z-[999]">
    <div class="max-w-6xl mx-auto px-6 py-4">
      <div class="flex items-center justify-between">
        <div class="font-semibold text-xl font-[plexMono] text-gray-400">{profile.name}</div>
        <div class="hidden md:flex space-x-8">
          <button on:click={() => scrollToSection('about')} class="text-gray-400 hover:text-[#8F4816] duration-300  transition-colors">About</button>
          <button on:click={() => scrollToSection('techStack')} class="text-gray-400 hover:text-[#FAC050ff] duration-300  transition-colors" class:text-gray-900={activeSection === 'techStack'}>Tech Stack</button>
          <button on:click={() => scrollToSection('projects')} class="text-gray-400 hover:text-[#B36673ff] duration-300  transition-colors" >Projects</button>
          <button on:click={() => scrollToSection('journey')} class="text-gray-400 hover:text-[#9471CBff] duration-300  transition-colors" >Education</button>
          <button on:click={() => scrollToSection('contact')} class="text-gray-400 hover:text-[#634a9b] duration-300 transition-colors" >Contact</button>
        </div>
      </div>
    </div>
  </nav>

  <!-- Sections -->
  <Hero {profile} />
  <Iam  {profile}  />
  <TechStack {techStack} />
  <Projects {projects} />
    <EducationCerts {experience} {education} {certifications} />
  <Contact {profile} />
  <Footer {profile} />
</div>

<style>
  :global(html) {
    scroll-behavior: smooth;
  }
</style>
