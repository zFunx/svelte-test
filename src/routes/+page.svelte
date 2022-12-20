<script>
	import { fade } from 'svelte/transition';

	// Components
	import FullPageImageGrid from '$lib/Components/ImageCollection/FullPageImageGrid.svelte';
	import ImageShowcase from '$lib/Components/ImageCollection/ImageShowcase.svelte';
	import Slideshow from '$lib/Components/ImageCollection/Slideshow.svelte';
	import CloseButton from '$lib/Components/ImageCollection/CloseButton.svelte';

	// Images
	import imageData from '../lib/data/image_data.json';
	const images = imageData[0].images;

	// Image state contro
	let imageActiveIndex = 0;
	const imageDisplayStates = {
		showcase: 'showcase',
		showall: 'showall',
		slideshow: 'slideshow'
	};
	let currentImageDisplayState = imageDisplayStates.showcase;
	const changeView = (displayState, activeIndex) => {
		if (typeof activeIndex !== 'undefined') {
			imageActiveIndex = activeIndex;
		}
		currentImageDisplayState = imageDisplayStates[displayState];
	};
</script>

{#if currentImageDisplayState == imageDisplayStates.showcase}
	<div class="hidden sm:block">
		<ImageShowcase {images} on:click={(e) => changeView('showall', e.detail)} />
	</div>
	<div class="cursor-pointer sm:hidden">
		<Slideshow
			{images}
			on:click={(e) => changeView('showall', e.detail)}
			activeIndex={imageActiveIndex}
		/>
	</div>
{:else if currentImageDisplayState == imageDisplayStates.showall}
	<FullPageImageGrid
		{images}
		activeIndex={imageActiveIndex}
		on:click={(e) => changeView('slideshow', e.detail)}
		on:close={() => changeView('showcase')}
	/>
{:else if currentImageDisplayState == imageDisplayStates.slideshow}
	<div
		transition:fade
		class="bg-black fixed top-0 bottom-0 left-0 right-0 flex items-center md:p-16"
	>
		<div class="md:rounded-lg overflow-hidden">
			<Slideshow {images} activeIndex={imageActiveIndex} />
		</div>
		<CloseButton className="fixed top-6 left-6" on:click={() => changeView('showall')} />
	</div>
{/if}
