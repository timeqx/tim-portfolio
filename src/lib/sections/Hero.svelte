<!-- Hero.svelte -->
<script>
	export let profile;
</script>

<section id="about" class="relative min-h-[92vh]  bg-[#131010] px-10">
	<!-- Floating Boxes -->
	<div class="absolute inset-0 z-20">
		<!-- Floating Animated Cubes -->
		<div class="group absolute -top-10 left-10 z-0 animate-[float_30s_ease-in-out_infinite]">
			<div
				class="h-24 w-24 rounded-lg bg-[#181616] shadow-[0_10px_15px_#8F4816ff] backdrop-blur-md transition-all
                duration-[3s] ease-out
               group-hover:shadow-[5px_-5px_25px_#FAC050ff]"
			></div>
		</div>

		<div class="group absolute top-40 left-30 z-0 animate-[float2_29s_ease-in-out_infinite] p-20">
			<div
				class="h-12 w-12 rounded-lg bg-[#181616] shadow-[0_-5px_15px_#FAC050ff] backdrop-blur-md transition-all
             duration-[3s] ease-out
               group-hover:shadow-[5px_5px_20px_#8F4816ff]"
			></div>
		</div>

		<div class="group absolute top-90 right-140 z-0 animate-[float2_28s_ease-in-out_infinite] p-20">
			<div
				class="h-20 w-20 rounded-lg bg-[#181616] shadow-[0_-5px_15px_#9471CBff] backdrop-blur-md transition-all
                duration-[3s] ease-out
                group-hover:shadow-[5px_5px_20px_#5A30B6ff]"
			></div>
		</div>

		

		<div class="group absolute top-150 right-40 z-0 animate-[float_26s_ease-in-out_infinite]">
			<div
				class="h-28 w-28 rounded-lg bg-[#181616] shadow-[0_12px_20px_#8b5cf6] backdrop-blur-md transition-all
               duration-[3s] ease-out
                group-hover:shadow-[6px_6px_35px_#d8b4fe]"
			></div>
		</div>
		<div class="group absolute top-30 right-170 z-0 animate-[float2_32s_ease-in-out_infinite]">
			<div
				class="h-8 w-8 rounded-lg bg-[#181616] shadow-[5px_0_10px_#B36673ff] backdrop-blur-md transition-all
               duration-[3s] ease-out
                group-hover:shadow-[-2px_-2px_15px_#9471CBff]"
			></div>
		</div>

		<div class="group absolute top-100 right-60 z-0 animate-[float2_40s_ease-in-out_infinite]">
			<div
				class="h-16 w-16 rounded-lg bg-[#181616] shadow-[10px_0_15px_#6b21a8] backdrop-blur-md transition-all
               duration-[3s] ease-out
               group-hover:shadow-[0_-10px_30px_#c084fc]"
			></div>
		</div>

	
	</div>

	<div class="absolute z-0 mx-auto flex max-w-6xl h-full justify-center items-center flex-row gap-20">
		<div class="w-3xl items-center justify-end flex">
     
      <div class="animate-[haloPulse_20s_ease-in_infinite] w-md p-20 z-10 rounded-full">
 <img src="timeqx.png" alt="Logo" class=" 
           animate-[shadowPulse_40s_ease-in_infinite]   " />
      </div>
   
    

		</div>
		<div class="mb-16 flex flex-col items-center justify-left">
			<h1 class="mb-6 w-full text-5xl font-bold text-gray-200 md:text-6xl animate-[glitch_2s_ease-in_infinite] ">
				{profile.name}
			</h1>
		<p class="md:text-1xl mb-8 text-left text-xl bg-gradient-to-r from-[#9471cbc2] via-[#B36673ff] to-[#fac15081] bg-clip-text text-transparent">
  Front to back, full stack — delivering modern cross-platform solutions with timeless performance.
</p>

		</div>
	</div>
</section>
