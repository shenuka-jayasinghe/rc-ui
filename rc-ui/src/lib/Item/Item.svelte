<script lang="ts">
	import About from '$lib/Item/About.svelte';
	import ImageViewer from '$lib/Item/ImageViewer.svelte';
	import Pages from '$lib/Item/Pages.svelte';
	import { TabGroup, Tab, TabAnchor } from '@skeletonlabs/skeleton';
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	let tabSet: number = 0;
    let pages: any[] = [];
    let metadataString = ''
    export let itemId: string
	let value = writable(1)
	// Subscribe to value changes and update the current value
    function updateValue(newValue: number) {
        value.set(newValue);
		console.log("newValue=====>", newValue)
		console.log("value=====>", $value)
    }

	$: {
		$value;
	}
	
	// let value = 1;

	


    onMount(async () => {
		try {
            // PR-INCU-03472
			console.log("itemId ==>", itemId)
			const response = await fetch(`http://localhost:3002/api/v1/json/${itemId}`);
			const data = await response.json();
			metadataString = data.JSON;
			const parsedJSON = JSON.parse(metadataString);
			pages = parsedJSON[0].pages;
		} catch (error) {
			console.error('Error fetching metadata', error);
		}
	});

	

</script>

<div class="container mx-auto">
	<div class="m-4 grid grid-cols-2 gap-4">
		<div>
			<ImageViewer
            {metadataString}
			value={$value}
            />
		</div>
		<div>
			<TabGroup>
				<Tab bind:group={tabSet} name="tab1" value={0}>
					<svelte:fragment slot="lead"></svelte:fragment>
					<span>About</span>
				</Tab>
				<Tab bind:group={tabSet} name="tab2" value={1}>Contents</Tab>
				<Tab bind:group={tabSet} name="tab3" value={2}>Pages</Tab>
				<!-- Tab Panels --->
				<svelte:fragment slot="panel">
					{#if tabSet === 0}
						<About 
                        {metadataString}
                        />
					{:else if tabSet === 1}
						No manifests here
					{:else if tabSet === 2}
						<Pages
                        {metadataString}
						{value}
						updateValue={updateValue}
                        />
					{/if}
				</svelte:fragment>
			</TabGroup>

		</div>
	</div>
</div>
