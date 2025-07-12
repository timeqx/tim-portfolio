<!-- Hero.svelte -->
<script>
	export let profile;
	import HeroCube from './HeroCube.svelte';
</script>

<section id="about" class="relative top-0 h-screen overflow-hidden bg-[#131010] px-10">
	<!-- Floating Boxes -->

	<HeroCube />

	<div
		class="absolute z-0 flex items-center justify-center h-full w-full "
	>
	<div class="flex h-1/2 w-3/4 flex-row items-center  justify-center gap-32">
		<div class="flex w-md items-center justify-end">
			<div class="z-10 animate-[haloPulse_20s_ease-in_infinite] rounded-full p-20"></div>
		</div>
		<div class="flex flex-col max-w-2xl items-center justify-center">
			<h1
				class="mb-6 w-full animate-[glitch_2s_ease-in_infinite] text-5xl text-gray-200 md:text-9xl  tracking-[2rem] "
			>
				{profile.name}
			</h1>
			<p
				class="md:text-1xl  bg-gradient-to-r from-[#9471cbc2] via-[#B36673ff] to-[#fac15081] bg-clip-text tracking-tight text-left text-xl text-transparent"
			>
				Front to back, full stack — delivering modern cross-platform solutions with timeless
				performance.
			</p>
		</div>
		</div>
	</div>
</section>

<style>
</style>
