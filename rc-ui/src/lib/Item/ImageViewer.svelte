<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { RangeSlider } from '@skeletonlabs/skeleton';
	import { readable } from 'svelte/store';
	let pages: any[] = [];
	let max = 1; //initialise to default value
	export let metadataString = ''

	$: {
        if (metadataString) {
            const parsedJSON = JSON.parse(metadataString);
            pages = parsedJSON[0].pages;
            max = pages.length;
        } else {
            pages = [];
            max = 1; // Reset to default value if metadataString is empty
        }
    }

    // Set a default value
    let value: number = 1;

</script>
{#if pages[value]}
<RangeSlider name="range-slider" bind:value max={pages.length} step={1} ticked>
	<div class="flex justify-between items-center">
		<div class="font-bold">
			{JSON.stringify(pages[value].label)}</div>
		<div class="text-xs"><input class="box-border h-[3px] w-[12px] bg-gray-800 text-white"/>/ {max}</div>
	</div>
</RangeSlider>
{/if}


<div>
    {#if pages[value]}
        <img class="rounded-t-md object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${pages[value].IIIFImageURL}/full/!2000,2000/0/default.jpg`} alt="" />
    {:else}
        <p>No data available for this index</p>
    {/if}
</div>
