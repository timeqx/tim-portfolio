<script>
	export let profile;
	
</script>

<section class="relative h-screen overflow-hidden bg-[#131010] px-4 md:px-10">
	

	<div class="absolute z-50 flex items-center justify-center h-full w-full">
		<div class="flex flex-col lg:flex-row items-center justify-center gap-12 lg:gap-32 h-full w-full max-w-7xl mx-auto">
			<!-- Left: Halo Effect -->
			<div class="relative z-10 flex items-center justify-center lg:w-1/2 w-full mb-10 lg:mb-0">
				<div class="animate-[haloPulse_20s_ease-in_infinite] rounded-full p-10 md:p-20 relative">
					<div class="absolute inset-0 opacity-10 z-10">
						<div class="absolute top-1/4 left-1/4 w-48 h-48 md:w-96 md:h-96 bg-gradient-to-r from-[#8F4816] to-[#FAC050ff] rounded-full blur-3xl"></div>
						<div class="absolute bottom-1/4 right-1/4 w-48 h-48 md:w-96 md:h-96 bg-gradient-to-r from-[#B36673ff] to-[#9471CBff] rounded-full blur-3xl"></div>
					</div>
				</div>
			</div>

			<!-- Right: Hero Text -->
			<div class="z-20 text-center lg:text-left max-w-xl px-4">
				<h1 class="mb-4 text-4xl sm:text-5xl md:text-6xl xl:text-7xl font-extrabold text-gray-200 font-[plexMono] animate-[glitch_2s_ease-in_infinite] tracking-widest">
					{profile.name}
				</h1>
				<p class="text-lg sm:text-xl md:text-2xl text-transparent bg-gradient-to-r from-[#9471cbc2] via-[#B36673ff] to-[#fac15081] bg-clip-text">
					Front to back, full stack — delivering modern cross-platform solutions with timeless performance.
				</p>
			</div>
		</div>
	</div>
</section>

