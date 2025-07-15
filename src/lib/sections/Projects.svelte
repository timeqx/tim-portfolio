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
	let projectCards = [];

	gsap.registerPlugin(ScrollTrigger, TextPlugin);

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

	function goToProject(index) {
		currentIndex = index;
		updateCarousel();
	}

	function updateCarousel() {
		gsap.to(carouselContainer, {
			x: -currentIndex * 100 + '%',
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
		updateCarousel();
	});
</script>

<section id="projects" class="relative flex items-center justify-center flex-col h-screen py-8 bg-gradient-to-br from-slate-50 to-gray-100">
	<!-- Section Label -->
	<div class="absolute top-1/2 right-10 -translate-y-1/2 rotate-90 z-10">
		<p class="text-3xl font-[plexMono] tracking-[0.3em] text-gray-800 uppercase">Projects</p>
	</div>

	<!-- Carousel Section -->
	<div class="relative max-w-5xl  mx-auto flex items-center justify-center">
		<!-- Left Arrow -->
		<button on:click={prevProject} class="btn btn-circle hover:btn-neutral mr-4" disabled={currentIndex === 0}>
			<FontAwesomeIcon icon={faArrowLeft} class="w-5 h-5" />
		</button>

		<!-- Carousel Track -->
		<div class="overflow-hidden w-[45rem] bg-[#131010] justify-start items-center flex h-[36rem] rounded-2xl">
			<div
				bind:this={carouselContainer}
				class="flex transition-transform  duration-700 w-2xl ease-out"
				
			>
				{#each projects as project, index}
					<div
						bind:this={projectCards[index]}
						class="w-2xl   px-6 flex-shrink-0 h-2xl "
					>
						<div class="bg-white h-full rounded-2xl shadow-lg hover:shadow-2xl transition duration-300 px-8 py-4 flex flex-col">
							<!-- Image -->
							<div class="h-72  rounded-lg">
								<img src={project.image} alt={project.title} class="w-full h-full object-contain" />
							</div>

							<!-- Title + Description -->
							<div class="flex-1">
								<h3 class="project-title text-xl font-bold text-gray-900 font-mono mb- opacity-0">
									{project.title}
								</h3>
								<p class="project-description text-sm text-gray-600 w-lg text-justify leading-relaxed mb-4 opacity-0">
									{project.description}
								</p>
							</div>

							<!-- Tech Stack -->
							<div class="flex flex-wrap gap-2 mb-3">
								{#each project.tech as tech}
									<span class="px-3 py-1 bg-gray-400 text-gray-800 text-sm rounded-md font-medium">
										{tech}
									</span>
								{/each}
							</div>

							<!-- Links -->
							<div class="flex space-x-4 pt-2">
							
								<a href={project.github} target="_blank" class="btn btn-sm {project.github ? '' : 'opacity-50 cursor-not-allowed'} "  aria-disabled={!project.github}>
										<svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
											<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"/>
										</svg>
									GitHub
								</a>
								
								
								<a href={project.demo} target="_blank" class="btn btn--primary bg-gray-700 btn-sm {project.demo ? '' : 'opacity-50 cursor-not-allowed'} "  aria-disabled={!project.demo} ><svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
											<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
										</svg>Demo</a>
										
							</div>
						</div>
					</div>
				{/each}
			</div>
		</div>

		<!-- Right Arrow -->
		<button on:click={nextProject} class="btn btn-circle hover:btn-neutral ml-4" disabled={currentIndex === projects.length - 1}>
			<FontAwesomeIcon icon={faArrowRight} class="w-5 h-5" />
		</button>
	</div>

	<!-- Dot Navigation -->
	<div class="flex justify-center space-x-2 mt-8 bg-[#131010] px-2 py-2 rounded-lg w-auto">
		{#each projects as _, index}
			<button
				on:click={() => goToProject(index)}
				class="w-3 h-3 rounded-full transition-colors duration-200"
				class:bg-[#FAC050ff]={currentIndex === index}
				class:bg-gray-300={currentIndex !== index}
			></button>
		{/each}
	</div>
</section>
