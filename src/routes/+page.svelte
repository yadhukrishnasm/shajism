<script>
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/ScrollTrigger';
	import ScrollSmoother from 'gsap/ScrollSmoother';

	import Hero from '$lib/hero.svelte';
	import About from '$lib/about.svelte';
	import Showcase from '$lib/showcase.svelte';
	import Footer from '$lib/footer.svelte';

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);
		ScrollTrigger.defaults({
			toggleActions: 'restart pause resume pause',
			scroller: '#smooth-content'
		});

		// About section (black background)
		ScrollTrigger.create({
			trigger: '#about',
			start: 'top 40%',
			end: 'bottom 40%',
			scroller: '#smooth-content',
			onEnter: () => gsap.to('#navbar', { color: '#fff', duration: 0.2 }),
			onLeaveBack: () => gsap.to('#navbar', { color: '#000', duration: 0.2 }),
			onLeave: () => gsap.to('#navbar', { color: '#000', duration: 0.2 }),
			onEnterBack: () => gsap.to('#navbar', { color: '#fff', duration: 0.2 })
		});

		// Footer section (black background)
		ScrollTrigger.create({
			trigger: '#footer',
			start: 'top 60%',
			end: 'bottom 100%',
			scroller: '#smooth-content',
			onEnter: () => gsap.to('#navbar', { color: '#fff', duration: 0.2 }),
			onLeaveBack: () => gsap.to('#navbar', { color: '#000', duration: 0.2 })
		});
	});

	function scrollToHero() {
		const hero = document.getElementById('hero');
		if (hero) {
			hero.scrollIntoView({ behavior: 'smooth' });
		}
	}
</script>

<div id="smooth-wrapper">
	<button id="navbar" type="button" class=" font-libre text-lg" on:click={scrollToHero}
		>CHITHRAM</button
	>
	<div id="smooth-content">
		<div class="page text-2xl text-black" id="hero"><Hero /></div>
		<div class="page" id="about"><About /></div>
		<div class="page" id="showcase"><Showcase /></div>
		<div class="page p-4" id="footer"><Footer /></div>
	</div>
</div>

<style>
	.page {
		width: 100%;
		height: 100vh;
		position: relative;
		overflow: hidden;
		scroll-snap-align: start;
	}
	#smooth-wrapper {
		background-color: #f9eae1;
	}

	#smooth-content {
		scroll-snap-type: y mandatory;
		overflow: auto;
		height: 100vh;
	}
	#navbar {
		background: transparent;
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 80px;
		display: flex;
		&:hover {
			text-decoration: underline;
		}
		transition: all 1s ease-in-out;
		font-weight: 500;
		padding-left: 5em;
		align-items: center;
		z-index: 1000;
		color: #000000;
		transition: color 0.2s;
		border: none;
		cursor: pointer;
	}
	@media (max-width: 640px) {
		#navbar {
			height: 60px;
			padding-left: 2em;
			font-size: small;
		}
	}
</style>
