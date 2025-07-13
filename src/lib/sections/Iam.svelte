<script lang="ts">
  import { onMount } from 'svelte'; 
  import  gsap  from 'gsap';
  import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
  import { TextPlugin } from 'gsap/dist/TextPlugin';

  export let profile;

  onMount(() => {
  gsap.registerPlugin(ScrollTrigger, TextPlugin);
   gsap.fromTo(
  '.photo1',
  { opacity: 0.9 },
  {
    scrollTrigger: {
      trigger: '.photo1',
      start: 'top 40%',
      end: 'bottom center',
      scrub: true, 
    },
    opacity: 0,
    ease: 'none',
  }
);
gsap.fromTo(
  '.photo2',
  { opacity: 0 },
  {
    scrollTrigger: {
      trigger: '.photo1',
      start: 'top 40%',
      end: 'top 90%',
      scrub: true,
    },
    opacity: 0.9,
    ease: 'none',
  }
);


  // text1 animation on scroll
  gsap.fromTo(
    '.text1',
    {
      opacity: 0,
      y: 20
    },{
    scrollTrigger: {
      trigger: '.text1',
      start: 'top 80%', 
      end: 'top 80%',
      toggleActions: 'play none none none', 
    },
 
    opacity: 0.9,
    y: 0,
    duration: 1
  });
  gsap.fromTo(
    '.text2',
    {
      opacity: 0,
      y: 20
    },
    {
    scrollTrigger: {
      trigger: '.text1',
      start: 'top 80%', 
      end: 'bottom 30%',
      toggleActions: 'play none none none', 
    },
   stagger:0.3,
    opacity: 0.9,
    y: 0,
    delay: 0.5,
    duration: 1
  });

});
</script>


<section class="bg-[#F4F3F2]  py-20  text-gray-900">
  <div class="absolute rotate-270">
    <p class="md:text-1xl  text-gray-500 font-semibold tracking-widest font-[plexMono] text-left text-xl ">WHO I AM</p>
  </div>
	<div class="mx-auto flex items-center  justify-between max-w-4xl   flex-col md:flex-row">
		<!-- Left: Definition Style -->
		<div class="w-lg">
			<div class="flex items-center gap-5">
				<p class="text1 font-serif text-3xl font-semibold tracking-widest text-[#5A30B6ff]">
					/ ' i am, ' /
				</p>
			</div>
			<span class="text2 text-4xl font-thin tracking-[1rem] text-black">Timothy Osorio,</span>
			<div class="mt-3 flex">
				<span class="text2 rounded bg-gray-900/20 px-2 py-1 text-sm font-medium text-gray-800"
					>Developer</span
				>
        
				<span class="text2 ml-3 text-base text-gray-600 italic"
					>disciplined, </span
				><span class="text2 ml-1 text-base text-gray-600 italic"
					>adaptable, </span
				>
        <span class="text2 ml-1 text-base text-gray-600 italic"
					>future-minded</span
				>
			</div>
			<div class="text2 text-md mt-3 space-y-4 text-justify leading-relaxed font-thin">
				<p>
					I'm a full stack developer with a knack for building <strong class="text-black"
						>timeless, cross-platform experiences</strong
					>. Whether it's websites, software, or mobile apps, I craft solutions with elegance,
					performance, and precision.
				</p>
				<p>
					From UI to backend, cloud to device — I design systems that not only work well, but <strong
						class="text-black">feel effortless to use</strong
					>.
				</p>
			</div>
		</div>

		<!-- Right: Screenshot-style visuals -->
		<div class="w-56 relative h-80 rounded-xl shadow-2xl ">
 	<img
				src="/holo.jpg"
				alt="bg"
				class="absolute h-[21rem] w-[18rem]  rounded-xl object-fill shadow-2xl"
			/>
      	<img
				src="/prof2.JPG"
				alt="Timothy Osorio"
				class="photo2 absolute h-[21rem] rounded-xl object-contain shadow-2xl"
			/>
			     <img
				src="/prof1.JPG"
				alt="Timothy Osorio"
				class="photo1 absolute h-[21rem]  rounded-xl object-contain shadow-2xl"
			/>
		</div>
	</div>
</section>
