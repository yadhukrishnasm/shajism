<script>
	import { onMount,onDestroy,tick } from 'svelte';

	const works = ['images/2', 'images/3', 'images/4', 'images/5'];

	let current = 0; // current image index
	let imgEl;
	let interval;

	onMount(async () => {
		const gsap = (await import('gsap')).default;
		const ScrollTrigger = (await import('gsap/ScrollTrigger')).default;
		gsap.registerPlugin(ScrollTrigger);

		// Start slideshow interval
		interval = setInterval(() => {
			if (!imgEl) return;
			const next = (current + 1) % works.length;

			gsap.to(imgEl, {
				opacity: 0,
				duration: 1.5,
				onComplete: () => {
					current = next;
					tick().then(() => {
						gsap.fromTo(imgEl, { opacity: 0 }, { opacity: 1, duration: 1 });
					});
				}
			});
		}, 8000);
	});
     onDestroy(() => clearInterval(interval));
</script>

<div class="about-container relative md:grid md:grid-cols-2">
	<div class="absolute">
		<img src="/svg/taj.svg" class="m-20 hidden h-60 md:block" alt="" />
	</div>
	<div id="aboutLeft" class="flex w-full flex-col justify-end gap-6 p-10 pt-20 md:p-20 md:pt-0">
		<p class="text-2xl font-bold md:text-5xl">
			Acrylic. <br /> Cartoon. <br /> Mural Art. <br />Wall painting.
		</p>
	</div>
	<div
		id="aboutRight"
		class="flex h-[100vh] scale-105 flex-wrap justify-center gap-3 overflow-hidden md:gap-6 border"
	>
		<img
			bind:this={imgEl}
			src={works[current]}
			alt={`painting-${current}`}
			class="absolute max-h-full w-full h-full object-cover"
		/>
	</div>
</div>
