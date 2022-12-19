<script>
	export let images = [];
</script>

<div class="flex overflow-auto snap-x snap-mandatory">
	{#each images as image, index (image.image_url)}
		<img  class="snap-center" src={image.image_url} alt={image.tags} loading="lazy" />
	{/each}
</div>
