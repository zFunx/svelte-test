<script>
	 export let images = [];
</script>

{#each images.slice(0, 5) as image, index (image.image_url)}
	<img
		class:row-span-2={0 == index}
		class:col-span-2={0 == index}
		class="h-full object-cover cursor-pointer transition-all brightness-100  hover:brightness-90"
		src={image.image_url}
		alt={image.tags}
	/>
{/each}
