<script>
	export let images = [];
	export let activeIndex = 0;

	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	const onClose = () => dispatch('close');
	const onClick = (index) => dispatch('click', index);

	// Components
	import CloseButton from '$lib/Components/ImageCollection/ImageGrid/CloseButton.svelte';

	const spanToFullIndex = 3; // Every third image with full width

	const refs = [];
	onMount(() => {
		refs[activeIndex].scrollIntoView({ behavior: 'auto' });
	});
</script>

<div
	transition:fade
	class="bg-white fixed top-0 bottom-0 left-0 right-0 md:py-4 md:px-12 overflow-auto"
>
	<div class="grid grid-cols-4 gap-2">
		{#each images as image, index (image.image_url)}
			<img
				class="h-full object-cover snap-center transition-all brightness-100 border-white cursor-pointer hover:brightness-90"
				class:col-span-2={0 != (index + 1) % spanToFullIndex}
				class:row-span-2={0 != (index + 1) % spanToFullIndex}
				class:col-span-4={0 == (index + 1) % spanToFullIndex}
				class:row-span-4={0 == (index + 1) % spanToFullIndex}
				bind:this={refs[index]}
				src={image.image_url}
				alt={image.tags}
				loading="lazy"
				on:click={onClick(index)}
			/>
		{/each}

		<CloseButton className="fixed top-6 left-6" on:click={onClose} />
	</div>
</div>
