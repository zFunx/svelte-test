<script>
	// Components
	import ImageGrid from '$lib/Components/ImageCollection/ImageGrid/ImageGrid.svelte';
	import Slideshow from '$lib/Components/ImageCollection/Slideshow/Slideshow.svelte';
	import SlideshowModal from '$lib/Components/ImageCollection/Slideshow/SlideshowModal.svelte';

	// Desktop
	// 1. (Completed) Create grid with CSS grid with show all button (simple)
	// 2. (Completed) Create grid with CSS grid in a modal

	// Mobile
	// 1. Create slideshow using scroll
	// 2. (Completed) Create grid with CSS grid in a modal
	// 1. Create slideshow using scroll

	// Make use of route and listing_id in

	import imageData from '../lib/data/image_data.json';
	const images = imageData[0].images;

	let expandImageGrid = false;
	const expandGrid = () => (expandImageGrid = true);
	const collapseGrid = () => (expandImageGrid = false);
</script>

<div class="sm:block" class:hidden={!expandImageGrid}>
	<ImageGrid {images} {expandImageGrid} on:collapse={collapseGrid} />
</div>
{#if !expandImageGrid}
	<div class="sm:hidden">
		<Slideshow {images} on:click={expandGrid} />
	</div>
{/if}
<!-- <SlideshowModal {images} /> -->
