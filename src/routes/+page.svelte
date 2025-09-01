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

		ScrollTrigger.create({
			trigger: '#hero',
			start: 'bottom center',
			onEnter: () => {
				gsap.to('#navbar', { y: 0, opacity: 1, duration: 0.4 });
			},
			onLeaveBack: () => {
				gsap.to('#navbar', { y: -100, opacity: 0, duration: 0.4, ease: 'power2.in' });
			}
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
	<button id="navbar" type="button" class="font-windsong text-2xl" on:click={scrollToHero}
		>Shaji S M</button
	>
	<div id="smooth-content">
		<div class="page text-2xl text-black" id="hero"><Hero /></div>
		<div class="page" id="showcase"><Showcase /></div>
		<div class="page" id="about"><About /></div>
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
		background-color: #f9f9f9;
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
		padding-left: 2em;
		align-items: center;
		z-index: 1000;
		color: #000000;
		transition: color 0.2s;
		border: none;
		transform: translateY(-100);
		opacity: 0;
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
