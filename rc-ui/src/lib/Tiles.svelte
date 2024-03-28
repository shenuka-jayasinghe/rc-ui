<script lang="ts">
	import { page } from "$app/stores";
	import { onMount } from "svelte";
    let pages: any[] = [];

    onMount(async () => {
        try{
            const response = await fetch('http://localhost:3002/api/v1/json/PR-INCU-03472');
        const data = await response.json();
        const metadataString = data.JSON;
        const parsedJSON = JSON.parse(metadataString);
        pages = parsedJSON[0].pages;
        }
        catch (error){
            console.error('Error fetching metadata', error)
        }
    })
</script>

<div class="flex flex-wrap">
    {#each pages as page}
        <div class="max-w-xs bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 m-5 transition-transform transform hover:scale-105 hover:shadow-2xl">
            <a href="/" class="card">
                <img class="rounded-t-md h-[200px] object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${page.IIIFImageURL}/full/!348,348/0/default.jpg`} alt="" />
            </a>
        </div>
    {/each}
</div>
    <!-- {JSON.stringify(pages)} -->
    