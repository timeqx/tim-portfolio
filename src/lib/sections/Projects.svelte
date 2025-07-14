<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
	import { TextPlugin } from 'gsap/dist/TextPlugin';

	export let projects;

	gsap.registerPlugin(ScrollTrigger, TextPlugin);

	onMount(() => {
		const projectsContainer = document.querySelector('.projects-container');
		const projectCards = document.querySelectorAll('.project-card');

		if (!projectsContainer || projectCards.length === 0) return;

		const scrollWidth = projectsContainer.scrollWidth;
		const scrollDistance = scrollWidth - window.innerWidth;

		const horizontalTl = gsap.timeline({
			scrollTrigger: {
				trigger: '.projects-wrapper',
				start: 'top top',
				end: () => `+=${scrollDistance}`,
				scrub: 1,
				pin: true,
				anticipatePin: 1
			}
		});

		horizontalTl.to(projectsContainer, {
			x: () => `-${scrollDistance}px`,
			ease: 'none'
		});

		projectCards.forEach((card) => {
			const title = card.querySelector('.project-title');
			const description = card.querySelector('.project-description');
			const techStack = card.querySelector('.tech-stack');
			const links = card.querySelector('.project-links');

			if (title) {
				gsap.fromTo(
					title,
					{ opacity: 0, text: '' },
					{
						scrollTrigger: {
							trigger: card,
							start: 'left center',
							end: 'left center',
							containerAnimation: horizontalTl,
							toggleActions: 'play none none reverse'
						},
						opacity: 1,
						text: title.getAttribute('data-text') ?? '',
						duration: 1,
						ease: 'power2.out'
					}
				);
			}

			if (description) {
				gsap.fromTo(
					description,
					{ opacity: 0, y: 30 },
					{
						scrollTrigger: {
							trigger: card,
							start: 'left center',
							end: 'left center',
							containerAnimation: horizontalTl,
							toggleActions: 'play none none reverse'
						},
						opacity: 1,
						y: 0,
						duration: 1,
						delay: 0.3,
						ease: 'power2.out'
					}
				);
			}

			if (techStack?.children) {
				gsap.fromTo(
					techStack.children,
					{ opacity: 0, scale: 0.8 },
					{
						scrollTrigger: {
							trigger: card,
							start: 'left center',
							end: 'left center',
							containerAnimation: horizontalTl,
							toggleActions: 'play none none reverse'
						},
						opacity: 1,
						scale: 1,
						duration: 0.5,
						stagger: 0.1,
						delay: 0.6,
						ease: 'back.out(1.7)'
					}
				);
			}

			if (links?.children) {
				gsap.fromTo(
					links.children,
					{ opacity: 0, x: -20 },
					{
						scrollTrigger: {
							trigger: card,
							start: 'left center',
							end: 'left center',
							containerAnimation: horizontalTl,
							toggleActions: 'play none none reverse'
						},
						opacity: 1,
						x: 0,
						duration: 0.8,
						stagger: 0.2,
						delay: 0.9,
						ease: 'power2.out'
					}
				);
			}
		});

		// Section title animation
		gsap.fromTo(
			'.section-title',
			{ opacity: 0, y: 20 },
			{
				scrollTrigger: {
					trigger: '.section-title',
					start: 'top 80%',
					end: 'top 80%',
					toggleActions: 'play none none none'
				},
				opacity: 1,
				y: 0,
				duration: 1
			}
		);

		// Label animation
		gsap.fromTo(
			'.projects-label',
			{ opacity: 0, y: 20 },
			{
				scrollTrigger: {
					trigger: '.projects-label',
					start: 'top 80%',
					end: 'bottom 30%',
					toggleActions: 'play none none none'
				},
				opacity: 1,
				y: 0,
				delay: 0.5,
				duration: 1
			}
		);
    
	});
</script>

<section id="projects" class="relative bg-[#F4F3F2] overflow-hidden">
	<div class="absolute top-20 right-0 rotate-90 z-10">
		<p class="projects-label md:text-1xl text-left font-[plexMono]  text-2xl font-semibold tracking-widest text-gray-500">
			PROJECTS
		</p>
	</div>

	<div class="projects-wrapper relative h-screen">
		<div class="projects-container flex h-full" style="width: {projects.length * 100}vw;">
			{#each projects as project}
				<div class="project-card w-screen h-full flex items-center justify-center px-8">
				{#if project.type === 'web'}
						<!-- Browser mockup for web projects -->
						<div class="mockup-browser border border-gray-300 bg-white w-full max-w-3xl mx-auto shadow-xl">
							<div class="mockup-browser-toolbar bg-gray-100">
								<div class="input border border-gray-300 bg-white text-gray-600 text-xs px-3 py-1 rounded">
									https://example.com
								</div>
							</div>
							<div class="bg-white p-4 max-h-[400px] overflow-y-auto">
								<div class="project-title text-xl font-bold text-gray-900 mb-2" data-text="{project.title}">
									{project.title}
								</div>
								<div class="project-description text-gray-600 mb-3 text-sm leading-relaxed">
									{project.description}
								</div>
								<div class="mb-3">
									<img src={project.image} alt="project screenshot" class="w-full h-32 object-cover rounded shadow-sm"/>
								</div>
								<div class="tech-stack mb-3 flex flex-wrap gap-1">
									{#each project.tech as tech}
										<span class="badge badge-outline badge-sm text-gray-700 px-2 py-1 text-xs">
											{tech}
										</span>
									{/each}
								</div>
								<div class="project-links flex space-x-3">
									<a
										href={project.github}
										target="_blank"
										rel="noopener noreferrer"
										class="btn btn-outline btn-primary btn-sm"
									>
										<svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
											<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"/>
										</svg>
										GitHub
									</a>
									<a
										href={project.demo}
										target="_blank"
										rel="noopener noreferrer"
										class="btn btn-primary btn-sm"
									>
										<svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
											<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
										</svg>
										Demo
									</a>
								</div>
							</div>
						</div>
					{:else if project.type === 'phone'}
						<!-- Phone mockup for mobile projects -->
						<div class="mockup-phone border-primary max-w-sm mx-auto">
							<div class="camera"></div>
							<div class="display">
								<div class="artboard artboard-demo phone-1 bg-white p-6">
									<div class="project-title text-2xl font-bold text-gray-900 mb-3 text-center" data-text="{project.title}">
										{project.title}
									</div>
									<div class="project-description text-gray-600 mb-4 text-sm leading-relaxed text-center">
										{project.description}
									</div>
									<div class="mb-4">
										<img src={project.image} alt="project screenshot" class="w-full rounded-lg shadow-md"/>
									</div>
									<div class="tech-stack mb-4 flex flex-wrap gap-2 justify-center">
										{#each project.tech as tech}
											<span class="badge badge-outline badge-sm text-gray-700">
												{tech}
											</span>
										{/each}
									</div>
									<div class="project-links flex flex-col space-y-2">
										<a
											href={project.github}
											target="_blank"
											rel="noopener noreferrer"
											class="btn btn-outline btn-primary btn-sm"
										>
											<svg class="w-4 h-4 mr-2" fill="currentColor" viewBox="0 0 20 20">
												<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"/>
											</svg>
											GitHub
										</a>
										<a
											href={project.demo}
											target="_blank"
											rel="noopener noreferrer"
											class="btn btn-primary btn-sm"
										>
											<svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
											</svg>
											Live Demo
										</a>
									</div>
								</div>
							</div>
						</div>
					{:else}
						<!-- Default card for other project types -->
						<div class="card w-full max-w-3xl mx-auto bg-white shadow-xl border border-gray-200">
							<div class="card-body p-4">
								<div class="project-title card-title text-xl font-bold text-gray-900 mb-2" data-text="{project.title}">
									{project.title}
								</div>
								<div class="project-description text-gray-600 mb-3 text-sm leading-relaxed">
									{project.description}
								</div>
								<div class="mb-3">
									<img src={project.image} alt="project screenshot" class="w-full h-32 object-cover rounded shadow-sm"/>
								</div>
								<div class="tech-stack mb-3 flex flex-wrap gap-1">
									{#each project.tech as tech}
										<span class="badge badge-outline badge-sm text-gray-700 px-2 py-1 text-xs">
											{tech}
										</span>
									{/each}
								</div>
								<div class="project-links card-actions justify-start">
									<a
										href={project.github}
										target="_blank"
										rel="noopener noreferrer"
										class="btn btn-outline btn-primary btn-sm"
									>
										<svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
											<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"/>
										</svg>
										GitHub
									</a>
									<a
										href={project.demo}
										target="_blank"
										rel="noopener noreferrer"
										class="btn btn-primary btn-sm"
									>
										<svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
											<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
										</svg>
										Demo
									</a>
								</div>
							</div>
						</div>
					{/if}

				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	.projects-wrapper {
		height: 100vh;
		position: relative;
		overflow: hidden;
	}

	.projects-container {
		display: flex;
		height: 100%;
		align-items: center;
	}

	.project-card {
		width: 100vw;
		height: 100vh;
		flex-shrink: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 0 2rem;
	}

	.card {
		max-height: 80vh;
		overflow-y: auto;
	}

	.project-title {
		font-family: 'Plex Mono', monospace;
	}
</style>
