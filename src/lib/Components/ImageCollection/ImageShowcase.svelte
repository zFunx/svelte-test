<script>
	export let images = [];

	// import { createEventDispatcher } from 'svelte';
	// const dispatch = createEventDispatcher();

	// Components
	import ShowAllBtn from '$lib/Components/ImageCollection/ImageGrid/ShowAllBtn.svelte';
</script>

<div class="my-4 mx-12 overflow-hidden relative rounded-lg">
	<div class="grid grid-cols-4 grid-flow-col gap-2">
		{#each images.slice(0, 5) as image, index (image.image_url)}
			<img
				class="h-full object-cover snap-center transition-all brightness-100 border-white cursor-pointer hover:brightness-90"
				class:col-span-2={0 == index}
				class:row-span-2={0 == index}
				src={image.image_url}
				alt={image.tags}
				loading="lazy"
			/>
		{/each}

		<ShowAllBtn className="absolute right-6 bottom-6" />
	</div>
</div>
