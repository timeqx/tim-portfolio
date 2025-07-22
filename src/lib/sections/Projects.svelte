<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
	import { TextPlugin } from 'gsap/dist/TextPlugin';

	import { faArrowLeft, faArrowRight } from '@fortawesome/free-solid-svg-icons';
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';

	export let projects;

	let currentIndex = 0;
	let carouselContainer: HTMLElement;
	let projectCards: HTMLElement[] = [];
	let isMobile = false;

	gsap.registerPlugin(ScrollTrigger, TextPlugin);

	function checkMobile() {
		isMobile = window.innerWidth < 768;
	}

	function nextProject() {
		if (currentIndex < projects.length - 1) {
			currentIndex++;
			updateCarousel();
		}
	}

	function prevProject() {
		if (currentIndex > 0) {
			currentIndex--;
			updateCarousel();
		}
	}

	function goToProject(index: number) {
		currentIndex = index;
		updateCarousel();
	}

	function updateCarousel() {
		const translateX = isMobile ? -currentIndex * 100 : -currentIndex * 100;
		gsap.to(carouselContainer, {
			x: translateX + '%',
			duration: 0.8,
			ease: 'power2.out'
		});

		if (projectCards[currentIndex]) {
			const title = projectCards[currentIndex].querySelector('.project-title');
			const description = projectCards[currentIndex].querySelector('.project-description');

			if (title) {
				gsap.fromTo(title, { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.6, delay: 0.2 });
			}
			if (description) {
				gsap.fromTo(description, { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.6, delay: 0.4 });
			}
		}
	}

	onMount(() => {
		checkMobile();
		updateCarousel();
		
		const handleResize = () => {
			checkMobile();
			updateCarousel();
		};
		
		window.addEventListener('resize', handleResize);
		return () => window.removeEventListener('resize', handleResize);
	});
</script>

<section id="projects" class="relative flex items-center justify-center flex-col min-h-screen py-4 md:py-8 px-4 md:px-0 bg-gradient-to-br from-slate-100 to-gray-200">
	<!-- Section Label - Hidden on mobile, visible on desktop -->
	<div class="hidden md:block absolute top-1/2 right-10 -translate-y-1/2 rotate-90 z-10">
		<p class="text-2xl font-[plexMono] tracking-[0.5em] text-gray-800 font-extrabold uppercase">Projects</p>
	</div>

	<!-- Mobile Section Title -->
	<div class="block md:hidden mb-2">
		<h2 class="text-3xl font-[plexMono] tracking-wider text-gray-800 font-extrabold uppercase text-center">Projects</h2>
	</div>

	<!-- Carousel Section -->
	<div class="relative  max-w-5xl mx-auto flex items-center justify-center">
		<!-- Desktop Navigation Arrows -->
		<button 
			on:click={prevProject} 
			class="hidden md:flex btn btn-circle hover:btn-neutral mr-4" 
			disabled={currentIndex === 0}
		>
			<FontAwesomeIcon icon={faArrowLeft} class="w-5 h-5" />
		</button>

		<!-- Carousel Track -->
		<div class="overflow-hidden w-full md:w-[45rem] bg-[#131010] justify-start items-center flex h-auto md:h-[36rem] rounded-2xl">
			<div
				bind:this={carouselContainer}
				class="flex transition-transform duration-700 ease-out w-[21rem] md:w-2xl"
				
			>
				{#each projects as project, index}
					<div
						bind:this={projectCards[index]}
						class="w-full px-3 md:px-6 flex-shrink-0 py-4 md:py-0"
					>
						<div class="bg-white h-full rounded-2xl shadow-lg hover:shadow-2xl transition duration-300 px-4 md:px-8 py-4 md:py-4 flex flex-col">
							<!-- Image -->
							<div class="h-44 md:h-72 rounded-lg mb-4 md:mb-0">
								<img src={project.image} alt={project.title} class="w-full h-full object-contain rounded-lg" />
							</div>

							<!-- Title + Description -->
							<div class="flex-1 mb-4">
								<h3 class="project-title text-md md:text-xl font-bold text-gray-900 font-mono mb-0 md:mb-3 opacity-0">
									{project.title}
								</h3>
								<p class="project-description text-xs md:text-sm text-gray-600 text-justify leading-relaxed mb-1 md:mb-4 opacity-0 line-clamp-4 md:line-clamp-none">
									{project.description}
								</p>
							</div>

							<!-- Tech Stack -->
							<div class="flex flex-wrap gap-2 mb-1 md:mb-4">
								{#each project.tech as tech}
									<span class="px-2 md:px-3 py-1 bg-gray-400 text-gray-800 text-xs md:text-sm rounded-md font-medium">
										{tech}
									</span>
								{/each}
							</div>

							<!-- Links -->
							<div class="flex flex-row gap-2 sm:space-x-4 sm:gap-0 pt-2">
								<a 
									href={project.github} 
									target="_blank" 
									class="btn btn-sm  {project.github ? '' : 'opacity-50 cursor-not-allowed'}" 
									aria-disabled={!project.github}
								>
									<svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
										<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"/>
									</svg>
									GitHub
								</a>
								
								<a 
									href={project.demo} 
									target="_blank" 
									class="btn btn-primary bg-gray-700 btn-sm   {project.demo ? '' : 'opacity-50 cursor-not-allowed'}" 
									aria-disabled={!project.demo}
								>
									<svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
									</svg>
									Demo
								</a>
							</div>
						</div>
					</div>
				{/each}
			</div>
		</div>

		<!-- Desktop Navigation Arrows -->
		<button 
			on:click={nextProject} 
			class="hidden md:flex btn btn-circle hover:btn-neutral ml-4" 
			disabled={currentIndex === projects.length - 1}
		>
			<FontAwesomeIcon icon={faArrowRight} class="w-5 h-5" />
		</button>
	</div>

	<!-- Mobile Navigation Arrows -->
	<div class="flex md:hidden justify-center space-x-4 mt-1">
		<button 
			on:click={prevProject} 
			class="btn btn-circle hover:btn-neutral" 
			disabled={currentIndex === 0}
		>
			<FontAwesomeIcon icon={faArrowLeft} class="w-4 h-4" />
		</button>
		
		<button 
			on:click={nextProject} 
			class="btn btn-circle hover:btn-neutral" 
			disabled={currentIndex === projects.length - 1}
		>
			<FontAwesomeIcon icon={faArrowRight} class="w-4 h-4" />
		</button>
	</div>

	<!-- Dot Navigation -->
	<div class="flex justify-center space-x-2 mt-2 md:mt-8 bg-[#131010] px-3 py-2 rounded-lg w-auto">
		{#each projects as _, index}
			<button
				on:click={() => goToProject(index)}
				class="w-2 h-2 md:w-3 md:h-3 rounded-full transition-colors duration-200"
				class:bg-[#FAC050ff]={currentIndex === index}
				class:bg-gray-300={currentIndex !== index}
			></button>
		{/each}
	</div>
</section>

<style>
	@media (max-width: 767px) {
		.line-clamp-4 {
			display: -webkit-box;
			-webkit-line-clamp: 4;
			-webkit-box-orient: vertical;
			overflow: hidden;
		}
	}
</style>