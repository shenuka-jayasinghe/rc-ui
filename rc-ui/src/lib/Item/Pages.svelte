<script lang="ts">
    export let metadataString: string;
    export let value: number = 0;
    export let updateValue: (newValue: number) => void; 
    import { RadioGroup, RadioItem } from '@skeletonlabs/skeleton';
    import { grid } from '$lib/assets/grid';
    import { carousel } from '$lib/assets/carousel'

    let pages: any[] = [];

    $: {
        if (metadataString) {
            const parsedJSON = JSON.parse(metadataString);
            pages = parsedJSON[0].pages;
        } else {
            pages = [];
        }
    }

    // Function to update the value when an anchor tag is clicked
	function handleClick(index: number) {
		const updatedValue = updateValue(index + 1); 
        // Call the updateValue function
    }
</script>

<div class="ml-2 mb-7">
    <RadioGroup>
        <RadioItem bind:group={value} name="justify" value={0}><svg class="fill-gray-400" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 -960 960 960" width="24">{@html grid}</svg></RadioItem>
        <RadioItem bind:group={value} name="justify" value={1}><svg class="fill-gray-400" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 -960 960 960" width="24">{@html carousel}</svg></RadioItem>
    </RadioGroup>
</div>

{#if value === 0}
<div class="flex flex-wrap">
    {#each pages as page, index}
        <div class="m-2">
            <a href="/" class="card" on:click|preventDefault={() => handleClick(index)}>
                <img class="rounded-t-md h-24 object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${page.IIIFImageURL}/full/!348,348/0/default.jpg`} alt="" />
            </a>
        </div>
    {/each}
</div>
{:else}
<div class="snap-x scroll-px-4 snap-mandatory scroll-smooth flex gap-4 overflow-x-auto px-4 py-10">
    {#each pages as page, index}
        <div class="snap-start shrink-0 card">
            <a href="/" class="card" on:click|preventDefault={() => handleClick(index)}>
                <img class="rounded-t-md h-96 object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${page.IIIFImageURL}/full/!348,348/0/default.jpg`} alt="" />
            </a>
            <br>
            <p class="text-center">Page {index + 1}</p>
        </div>
    {/each}
</div>

{/if}


