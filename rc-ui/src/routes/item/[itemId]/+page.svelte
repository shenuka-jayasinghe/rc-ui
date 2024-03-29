<script lang="ts">
	import About from '$lib/Item/About.svelte';
	import ImageViewer from '$lib/Item/ImageViewer.svelte';
	import Item from '$lib/Item/Item.svelte';
	import Pages from '$lib/Item/Pages.svelte';
	import { page } from '$app/stores';
	import { TabGroup, Tab, TabAnchor } from '@skeletonlabs/skeleton';
	let tabSet: number = 0;
	export const itemId = $page.params.itemId;
</script>

<Item
	itemId={itemId}
/>
