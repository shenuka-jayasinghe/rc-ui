<script lang="ts">
	import { writable } from 'svelte/store';
	import Item from '$lib/Item/Item.svelte';
	import { page } from '$app/stores';
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


<Item
metadataString={$metadataString}
 />
