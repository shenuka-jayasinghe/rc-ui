<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { RangeSlider } from '@skeletonlabs/skeleton';
	import { readable } from 'svelte/store';
    import { arrowBack } from '$lib/assets/arrowBack';
    import { arrowForward } from '$lib/assets/arrowForward';
	let pages: any[] = [];
	let max = 1; //initialise to default value
	export let metadataString = ''

    // Set a default value
    export let value: number = 1;

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


    function updateValue(event:any) {
        value = parseInt(event.target.value);
    }

    function pageForward() {
        value++
    }

    function pageBackward() {
        value--
    }


</script>


<div>
    <div class="flex justify-center btn-group !bg-transparent">
        <button on:click={pageBackward}><svg class="fill-current" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 -960 960 960" width="24">{@html arrowBack}</svg></button>
        <button><div>
            <div class="text-s flex items-center justify-center">
                <input type="number" id="page-number" name="page-number" required minlength="1" maxlength="8" class="box-border h-[3px] w-[70px] bg-gray-800 text-white" bind:value={value} on:input={updateValue}/>
                <span>/ {max}</span>
            </div>    
        </div></button>
        <button on:click={pageForward}><svg class="fill-current" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 -960 960 960" width="24">{@html arrowForward}</svg></button>
    </div>
    
    {#if pages[value]}
        <img class="rounded-t-md object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${pages[value-1].IIIFImageURL}/full/!2000,2000/0/default.jpg`} alt="" />
    {:else}
        <p>No data available for this index</p>
    {/if}
</div>
