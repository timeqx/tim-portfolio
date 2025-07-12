<!-- Hero.svelte -->
<script>
	export let profile;
	 import HeroCube from "./HeroCube.svelte";

</script>

<style>
	
</style>

<section id="about" class="relative min-h-[92vh]  bg-[#131010] px-10 ">
	<!-- Floating Boxes -->
	<HeroCube />

	<div class="absolute z-0 mx-auto flex max-w-6xl h-full justify-center items-center flex-row gap-20">
		<div class="w-3xl items-center justify-end flex">
     
      <div class="animate-[haloPulse_20s_ease-in_infinite] p-20 z-10 rounded-full">
 
      </div>
   
    

		</div>
		<div class="mb-16 flex flex-col items-center justify-left ">
			<h1 class="mb-6 w-full text-5xl font-bold text-gray-200 md:text-6xl animate-[glitch_2s_ease-in_infinite] ">
				{profile.name}
			</h1>
		<p class="md:text-1xl mb-8 text-left text-xl bg-gradient-to-r from-[#9471cbc2] via-[#B36673ff] to-[#fac15081] bg-clip-text text-transparent ">
  Front to back, full stack — delivering modern cross-platform solutions with timeless performance.
</p>

		</div>
	</div>
</section>
