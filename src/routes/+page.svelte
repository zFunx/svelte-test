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
</script>

<div class="hidden sm:block">
    <ImageGrid {images} />
</div>
<!-- <div class="sm:hidden">
    <Slideshow {images} />
</div> -->
<SlideshowModal {images} />


