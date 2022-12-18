<script>
    // Desktop
    // 1. Create grid with CSS grid with show all button (simple)
    // 2. Create grid with CSS grid in a modal
    // 3. Create slideshow using svelte transitions
    // 4. Add masonry to the grid in modal

    // Mobile
    // 1. Create slideshow using scroll
    // 2. Create grid with CSS grid in a modal
    // 1. Create slideshow using scroll

    // Make use of route and listing_id in 

    import imageData from '../lib/data/image_data.json'
    const images = imageData[0].images;
    
    console.log('imageData', images);
</script>

{#each images as image (image.image_url)}
    <img src={image.image_url} alt={image.tags} />
{/each}

