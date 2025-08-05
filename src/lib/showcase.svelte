<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	const cardCount = 7;
	const images = [
		'/images/12.jpg',
		'/images/13.jpg',
		'/images/14.jpg',
		'/images/15.jpg',
		'/images/16.jpg',
		'/images/19.jpg',
		'/images/21.jpg'
	];

	onMount(async () => {
		const gsap = (await import('gsap')).default;
		const ScrollTrigger = (await import('gsap/ScrollTrigger')).default;
		gsap.registerPlugin(ScrollTrigger);
		const isSmallDevice = window.innerWidth <= 640;
		const spread = isSmallDevice ? 40 : 130; // distance between each card

		gsap.fromTo(
			'.card',
			{
				x: 0,
				y: 0,
				rotate: 0,
				boxShadow: '0 0 0 rgba(0,0,0,0)'
			},
			{
				x: (i) => (i - (cardCount - 1) / 2) * spread,
				y: (i) => Math.abs(i - (cardCount - 1) / 2) * 10,
				rotate: (i) => (i - (cardCount - 1) / 2) * 5,
				boxShadow: '20px 20px 34px rgba(0,0,0,0.15)',
				borderRadius: '10px',
				duration: 1.5,
				ease: 'power3.out',
				stagger: 0.07,
				scrollTrigger: {
					trigger: '#showcaseContainer',
					start: 'top 80%',
					scroller: '#smooth-content',
					toggleActions: 'play none none none'
				}
			}
		);
	});
	let animating = false;

	async function handleLogin() {
		if (animating) return;
		animating = true;
		const gsap = (await import('gsap')).default;
		await gsap.to('#showcaseContainer', { opacity: 0, duration: 0.5 });
		goto('/login');
	}
</script>

<div id="showcaseContainer" class="px- pt-20 md:space-y-6 md:p-20">
	<div id="heading" class="text-center">
		<p class="font-instrument text-center text-3xl md:text-6xl" style="letter-spacing: 1px;">
			A Place To Display Your <br /> Masterpiece
		</p>
	</div>
	<div id="Cards-container" class="relative flex h-48 items-center justify-center md:h-[40vh]">
		{#each Array(cardCount) as _, i}
			<div class="card absolute h-28 w-28 border bg-white md:h-48 md:w-48">
				<img
					src={images[i]}
					alt="Artwork {i + 1}"
					class="h-full w-full rounded-[10px] object-cover"
				/>
			</div>
		{/each}
	</div>
	<div id="quote" class="mt-10 flex flex-col space-y-1 text-center italic md:mt-0">
		<p>“Art is the lie that enables us to realize the truth."</p>
		<p class="ml-40">- pablo picasso</p>
	</div>
	<div id="subheading" class="mt-15 flex flex-col space-y-2 text-center md:mt-0 md:block">
		<button
			class="m-3 rounded-full border bg-red-500 px-4 py-2 text-white md:mr-7"
			on:click={handleLogin}>Login/Register</button
		>
		<button class="underline">Read more</button>
	</div>
</div>

<style>
	#Cards-container {
		width: 100%;
	}
	.card {
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		transition: box-shadow 0.3s;
	}
</style>
