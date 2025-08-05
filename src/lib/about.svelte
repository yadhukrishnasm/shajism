<script>
    import { onMount } from 'svelte';


    const artTags = [
        "Painting", "Sculpture", "Digital Art", "Textile", "Embroidery",
        "Woodwork", "Collage", "Terracotta", "Photography",
        "Traditional", "Tribal", "Abstract", "Minimalist", "Realism",
        "Conceptual", "Folk", "Mural", "Geometric",
        "Madhubani", "Warli", "Gond", "Pattachitra", "Kerala Mural",
        "Chola Bronze", "Kalamkari", "Blue Pottery", "Dhokra",
        "For Sale", "Portfolio", "Exhibition", "Commission Work",
        "Open for Collaboration", "Storytelling Art", "Home Decor",
        "Ritual Art", "Cultural Art",
        "Emerging Artist", "Hobbyist", "Professional", "Student",
        "Rural Artisan", "Collective", "Independent Creator"
    ];

    onMount(async () => {
    const gsap = (await import('gsap')).default;
    const ScrollTrigger = (await import('gsap/ScrollTrigger')).default;
    gsap.registerPlugin(ScrollTrigger);

    gsap.from(".tag", {
        y: -100,
        opacity: 0,
        duration: 2,
        ease: "power3.out",
        stagger: 0.07,
        scrollTrigger: {
            trigger: "#aboutRight",
            start: "top 80%",
            scroller: "#smooth-content", 
            toggleActions: "play none none none"
        }
    });
});
</script>

<div class="about-container relative md:grid md:grid-cols-2 text-white bg-black">
    <div class="absolute">
        <img src="/svg/taj.svg" class="h-60 m-20 hidden md:block" alt="">
    </div>
    <div id="aboutLeft" class="flex w-full md:p-20 p-10 md:pt-0 pt-20 justify-end flex-col gap-6">
        <p class="md:text-5xl text-2xl font-bold">Your canvas online. <br> Discover. <br>Connect. <br>Create.</p>
    </div>
    <div id="aboutRight" class="flex flex-wrap md:gap-6 gap-3 justify-center scale-105 h-[100vh] overflow-hidden">
        {#each artTags as tag}
            <div class="tag md:px-5 md:py-3 px-3 py-2 font-extralight border rounded-full w-fit md:text-3xl hover:bg-[#FAF9F6] hover:text-black transition-colors duration-2000">{tag}</div>
        {/each}
    </div>
</div>
