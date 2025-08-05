<script>
	import '../app.css';
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	let { children } = $props();
</script>

{@render children()}
