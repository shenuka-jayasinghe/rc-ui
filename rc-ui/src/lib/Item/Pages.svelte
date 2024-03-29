<script lang="ts">
	import { page } from "$app/stores";
	import { onMount } from "svelte";
    import { readable } from "svelte/store";
    let pages: any[] = [];
    export let metadataString = ''

	const parsedMetadata = readable([], (set) => {
		if (metadataString) {
			const parsedJSON = JSON.parse(metadataString);
			set(parsedJSON[0].pages);
		} else {
			set([]);
		}
	});

	$: {
		pages = $parsedMetadata;
	}

</script>


<div class="snap-x scroll-px-4 snap-mandatory scroll-smooth flex gap-4 overflow-x-auto px-4 py-10">
	{#each pages as page, index}
		<div class="snap-start shrink-0 card"><a href="/" class="card">
            <img class="rounded-t-md h-[400px] object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${page.IIIFImageURL}/full/!348,348/0/default.jpg`} alt="" />
        </a>
        <br>
        <p class="text-center">Page {index + 1}</p>
        </div>
        

	{/each}
</div>

    <!-- {JSON.stringify(pages)} -->
    
    