<script>
	export let images = [];
	export let expandImageGrid = false;

	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	// Components
	import ShowAllBtn from '$lib/Components/ImageCollection/ImageGrid/ShowAllBtn.svelte';
	import CloseButton from './CloseButton.svelte';
	import SlideshowModal from '../Slideshow/SlideshowModal.svelte';

	// Expand/collapse grid
	// let expandImageGrid = false;
	const toggleImageGridExpansion = () => {
		if (expandImageGrid) {
			dispatch('collapse');
		}
		expandImageGrid = !expandImageGrid;
	};

	let activeIndex = -1;
	const setActiveIndex = (index) => {
		activeIndex = index;
		isModelOpen = true
	};

	let isModelOpen = false;
</script>

<div
	class={`${
		expandImageGrid
			? 'bg-white md:pt-24 md:pb-4 md:px-12 top-0 bottom-0 left-0 right-0 overflow-auto fixed snap-y snap-mandatory'
			: 'my-4 mx-12 overflow-hidden relative rounded-lg'
	} `}
>
	<div class="grid grid-cols-4 gap-2 grid-flow-dense">
		{#each images.slice(0, expandImageGrid ? images.length : 5) as image, index (image.image_url)}
			<img
				class={`${
					index % 3 == 0 && expandImageGrid ? 'w-full' : 'h-full'
				} object-cover snap-center transition-all brightness-100 border-white cursor-pointer hover:brightness-90
                    ${
											'row-span-' +
											[expandImageGrid ? (index % 3 == 0 ? 4 : 2) : 0 == index ? 2 : 1]
										}
                    ${
											'col-span-' +
											[expandImageGrid ? (index % 3 == 0 ? 4 : 2) : 0 == index ? 2 : 1]
										}`}
				src={image.image_url}
				alt={image.tags}
				on:click={expandImageGrid ? setActiveIndex(index) : toggleImageGridExpansion()}
				loading="lazy"
			/>
		{/each}

		{#if !expandImageGrid}
			<ShowAllBtn className="absolute right-6 bottom-6" on:click={toggleImageGridExpansion} />
		{:else}
			<CloseButton className="fixed top-6 left-4 md:left-8" on:click={toggleImageGridExpansion} />
		{/if}
	</div>
</div>

{#if isModelOpen}
<SlideshowModal {images} />
{/if}


