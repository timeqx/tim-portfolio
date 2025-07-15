<!-- Hero.svelte -->
<script>
	export let profile;
	import HeroCube from './HeroCube.svelte';
</script>

<section id="about" class="relative top-0 h-screen overflow-hidden bg-[#131010] px-10">
	<!-- Floating Boxes -->

	<HeroCube />

	<div
		class="absolute z-50 flex items-center justify-center h-full w-full "
	>
	<div class="flex h-1/2 w-3/4 flex-row items-center  justify-center gap-32 z-50">
		<div class="flex w-md items-center justify-end">
			<div class="z-10 animate-[haloPulse_20s_ease-in_infinite] rounded-full p-20 relative"><!-- Animated background elements -->
  <div class="absolute inset-0 opacity-10 z-10">
    <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-gradient-to-r from-[#8F4816] to-[#FAC050ff] rounded-full blur-3xl"></div>
    <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-gradient-to-r from-[#B36673ff] to-[#9471CBff] rounded-full blur-3xl"></div>
  </div></div>
		</div>
		<div class="flex flex-col max-w-2xl items-center justify-center">
			<h1
				class="mb-6 w-full animate-[glitch_2s_ease-in_infinite] text-5xl text-gray-200 md:text-9xl  tracking-[2rem] font-extrabold font-[plexMono] "
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
