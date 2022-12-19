<script>
	export let images = [];

	// Components
	import ShowAllBtn from '$lib/Components/ImageCollection/ImageGrid/ShowAllBtn.svelte';

	// Expand/collapse grid
	let expandImageGrid = false;
	const toggleImageGridExpansion = () => (expandImageGrid = !expandImageGrid);

	// Modify images with spans
	images = images.map((img, index) => ({
		...img,
		rowSpan: index % 3 == 0 ? 4 : 2,
		colSpan: index % 3 == 0 ? 4 : 2
	}));

	let activeIndex = -1;
	const setActiveIndex = (index) => (activeIndex = index);
</script>

<div
	class={`${
		expandImageGrid
			? 'bg-white pt-16 pb-4 px-12 top-0 bottom-0 left-0 right-0 overflow-auto fixed'
			: 'my-4 mx-12 overflow-hidden relative'
	} rounded-lg`}
>
	<div class="grid grid-cols-4 gap-2 grid-flow-dense">
		{#each images.slice(0, expandImageGrid ? images.length : 5) as image, index (image.image_url)}
			<img
				class={`h-full object-cover transition-all brightness-100 border-white cursor-pointer hover:brightness-90
                    ${'row-span-' + [expandImageGrid ? image.rowSpan : 0 == index ? 2 : 1]}
                    ${'col-span-' + [expandImageGrid ? image.colSpan : 0 == index ? 2 : 1]}`}
				src={image.image_url}
				alt={image.tags}
				on:click={setActiveIndex(index)}
			/>
		{/each}

		{#if !expandImageGrid}
			<ShowAllBtn className="absolute right-6 bottom-6" on:click={toggleImageGridExpansion} />
		{/if}
	</div>
</div>
