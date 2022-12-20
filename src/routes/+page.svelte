<script>
	// Components
	import { fade } from 'svelte/transition';

	import FullPageImageGrid from '$lib/Components/ImageCollection/FullPageImageGrid.svelte';
	import ImageGrid from '$lib/Components/ImageCollection/ImageGrid/ImageGrid.svelte';
	import ImageShowcase from '$lib/Components/ImageCollection/ImageShowcase.svelte';
	import Slideshow from '$lib/Components/ImageCollection/Slideshow/Slideshow.svelte';
	import SlideshowModal from '$lib/Components/ImageCollection/Slideshow/SlideshowModal.svelte';
	// Components
	import CloseButton from '$lib/Components/ImageCollection/ImageGrid/CloseButton.svelte';
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

	const imageDisplayStates = {
		showcase: 'showcase',
		showall: 'showall',
		slideshow: 'slideshow'
	};
	let currentImageDisplayState = imageDisplayStates.showcase;
	// const showShowcase = () => (currentImageDisplayState = imageDisplayStates.showcase);
</script>

{#if currentImageDisplayState == imageDisplayStates.showcase}
	<div class="hidden sm:block">
		<ImageShowcase
			{images}
			on:click={() => (currentImageDisplayState = imageDisplayStates.showall)}
		/>
	</div>
	<div
		class="cursor-pointer sm:hidden"
		on:click={() => (currentImageDisplayState = imageDisplayStates.showall)}
	>
		<Slideshow {images} />
	</div>
{:else if currentImageDisplayState == imageDisplayStates.showall}
	<FullPageImageGrid
		{images}
		on:click={() => (currentImageDisplayState = imageDisplayStates.slideshow)}
		on:close={() => (currentImageDisplayState = imageDisplayStates.showcase)}
	/>
{:else if currentImageDisplayState == imageDisplayStates.slideshow}
	<div
		transition:fade
		class="bg-black fixed top-0 bottom-0 left-0 right-0 flex items-center md:p-16"
	>
		<div class="md:rounded-lg overflow-hidden">
			<Slideshow {images} />
		</div>
		<CloseButton
			className="fixed top-6 left-6"
			on:click={() => (currentImageDisplayState = imageDisplayStates.showall)}
		/>
	</div>
{/if}
