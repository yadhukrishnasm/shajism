<script>
	import gsap from "gsap";
	import { onMount } from "svelte";

	onMount(() => {
		const tl = gsap.timeline();

		// Animate each word separately with stagger
		tl.fromTo(
			".role-word",
			{ y: 50, opacity: 0 },
			{
				y: 0,
				opacity: 1,
				duration: 1,
				stagger: 0.8,
				ease: "power3.out"
			}
		)

			// After all visible, slide whole line up + vanish
			.to(".role-line", {
				y: -80,
				opacity: 0,
				duration: 1,
				delay: 1,
				ease: "power2.in"
			})

			// Final name in
			.fromTo(
				".final-name",
				{ y: 50, opacity: 0 },
				{ y: 15, opacity: 1, duration: 1.2, ease: "power3.out" }
			);
	});
</script>

<div class="border">
	
</div>

<div class="center-text  md:mb-0">
	<p class="font-instrument text-6xl relative overflow-hidden h-22 ">
		<span class="role-line inline-flex gap-4">
			<span class="role-word">Painter /</span>
			<span class="role-word">Designer /</span>
			<span class="role-word">Artist</span>
		</span>
		<span class="final-name absolute font-windsong inset-0 text-6xl ">Shaji S M</span>
	</p>
	<p class="font-libre text-sm italic ">From <b>Kerala</b> India</p>
</div>

<style>
	.center-text {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: 2;
		text-align: center;
	}

	.role-word {
		opacity: 0;
		display: inline-block;
	}

	.final-name {
		opacity: 0;
		text-align: center;
	}
</style>
