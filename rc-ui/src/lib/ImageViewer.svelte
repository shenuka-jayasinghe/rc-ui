<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { RangeSlider } from '@skeletonlabs/skeleton';
	let pages: any[] = [];
	let max = 1; //initialise to default value

	onMount(async () => {
		try {
			const response = await fetch('http://localhost:3002/api/v1/json/PR-INCU-03472');
			const data = await response.json();
			const metadataString = data.JSON;
			const parsedJSON = JSON.parse(metadataString);
			pages = parsedJSON[0].pages;
		} catch (error) {
			console.error('Error fetching metadata', error);
		}
	});
	let value = 1;
	$: {
		max = pages.length;
	}
</script>

<RangeSlider name="range-slider" bind:value max={25} step={1} ticked>
	<div class="flex justify-between items-center">
		{#if pages[value]}
		<div class="font-bold">
			{JSON.stringify(pages[value].label)}</div>
		{:else}
		<div class="font-bold">
			Label</div>
		{/if}

		<div class="text-xs">{value} / {max}</div>
	</div>
</RangeSlider>

<div>
    {#if pages[value]}
        <img class="rounded-t-md object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${pages[value].IIIFImageURL}/full/!2000,2000/0/default.jpg`} alt="" />
    {:else}
        <p>No data available for this index</p>
    {/if}
</div>
