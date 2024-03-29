<script lang="ts">
    import { derived } from 'svelte/store';

    let metadata: any[] = [];
    let labels: { label: any; value: any }[] = [];

    // Define a variable to hold the metadata string
    export let metadataString: string;

    // Function to parse metadata and update labels
    function parseMetadata(metadataString: string) {
        const parsedJSON = JSON.parse(metadataString);
        metadata = parsedJSON[0].descriptiveMetadata;
        
        labels = metadata.reduce((acc, obj) => {
            for (let key in obj) {
                if (obj[key]?.hasOwnProperty('label') && obj[key]?.hasOwnProperty('value')) {
                    const label = obj[key].label;
                    const value = obj[key].value[0].displayForm;
                    acc.push({ label: label, value: value });
                }
            }
            return acc;
        }, []);
    }

    // Parse metadataString when it changes
    $: {
        if (metadataString) {
            parseMetadata(metadataString);
        }
    }

    // Create a derived store for metadataString
    $: metadataStringStore = derived([metadata], ([$metadata]) => {
        return JSON.stringify($metadata);
    });
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