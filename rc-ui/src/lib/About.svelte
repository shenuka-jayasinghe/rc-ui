<script lang="ts">
    import { onMount } from 'svelte';
	import { writable } from 'svelte/store';

	let metadata: any[] = [];
	let labels: { label: any; value: any }[] = [];

    // Create a writable store for the labels
	const labelsStore = writable(labels);

onMount(async () => {
    try {
        const response = await fetch('http://localhost:3002/api/v1/json/PR-INCU-03472');
        const data = await response.json();
        const metadataString = data.JSON;
        const parsedJSON = JSON.parse(metadataString);
        metadata = parsedJSON[0].descriptiveMetadata;

        metadata.forEach((obj: any) => {
            for (let key in obj) {
                if (obj[key]?.hasOwnProperty('label') && obj[key]?.hasOwnProperty('value')) {
                    const label = obj[key].label;
                    const value = obj[key].value[0].displayForm;
                    labels.push({ label: label, value: value });
                }
            }
        });

        // Update the labels store with the new labels array
        labelsStore.set(labels);
    } catch (error) {
        console.error('Error fetching metadata:', error);
    }
});

// Subscribe to changes in the labels store and update the local labels variable
$: {
    const unsubscribe = labelsStore.subscribe((newLabels) => {
        labels = newLabels;
    });
    
}
</script>

<div class = 'm-1'>
    {#if labels.length > 0}
        {#each labels as item}
            <strong>{item.label}:</strong> {@html item.value}
            <br>
        {/each}
    {:else}
        <p>No labels to display.</p>
    {/if}
</div>