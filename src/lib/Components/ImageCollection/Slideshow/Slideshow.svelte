<script>
	export let images = [];

	let frScrolled = 1 / images.length;
	function onScroll(e) {
		const elem = e.target;
		const scrollWidth = elem.scrollWidth;
		const scrolled = elem.scrollLeft;
		frScrolled = (scrolled + window.screen.width) / scrollWidth;
	}

	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

    const onClick = () => dispatch('click')
</script>

<div class="relative">
	<div class="flex overflow-auto snap-x snap-mandatory" on:scroll={onScroll}>
		{#each images as image, index (image.image_url)}
			<img on:click={onClick} class="snap-center" src={image.image_url} alt={image.tags} loading="lazy" />
		{/each}
		<div class="absolute bottom-4 right-4 bg-black rounded-xl px-2 py-2 text-white">
			{Math.ceil(frScrolled * images.length)}/{images.length}
		</div>
	</div>
</div>
