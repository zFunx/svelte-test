<script>
	export let images = [];
</script>

<div
	class="bg-black fixed top-0 bottom-0 left-0 right-0 flex items-center overflow-auto snap-x snap-mandatory justify-around gap-[20%]"
>
	{#each images as image, index (image.image_url)}
		<img class="snap-center rounded w-4/5" src={image.image_url} alt={image.tags} loading="lazy" />
	{/each}
</div>
