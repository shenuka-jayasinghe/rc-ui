<script lang="ts">
	import { writable } from 'svelte/store';
	import About from '$lib/Item/About.svelte';
	import ImageViewer from '$lib/Item/ImageViewer.svelte';
	import Item from '$lib/Item/Item.svelte';
	import Pages from '$lib/Item/Pages.svelte';
	import { page } from '$app/stores';
	import { TabGroup, Tab, TabAnchor } from '@skeletonlabs/skeleton';
	import { onMount } from 'svelte';

	let tabSet: number = 0;
	export const itemId = $page.params.itemId;
	let metadataString = writable('');
	let pages = [];

	onMount(async () => {
		try {
			const response = await fetch(`http://localhost:3002/api/v1/json/${itemId}`);
			const data = await response.json();
			metadataString.set(data.JSON); // Update the value of metadataString using its set method
			const parsedJSON = JSON.parse(data.JSON);
			pages = parsedJSON[0].pages;
		} catch (error) {
			console.error('Error fetching metadata', error);
		}
	});
	
</script>

<Item itemId={itemId}
metadataString={$metadataString}
 />
