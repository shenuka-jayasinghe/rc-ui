<script lang="ts">
    export let metadataString: string;
    export let value: any;
    export let updateValue: (newValue: number) => void; 

    let pages: any[] = [];

    $: {
        if (metadataString) {
            const parsedJSON = JSON.parse(metadataString);
            pages = parsedJSON[0].pages;
        } else {
            pages = [];
        }
    }

    // Function to update the value when an anchor tag is clicked
	function handleClick(index: number) {
		console.log("pages index ===> ",index + 1)
		const updatedValue = updateValue(index + 1); 
        // Call the updateValue function
    }
</script>

<div class="snap-x scroll-px-4 snap-mandatory scroll-smooth flex gap-4 overflow-x-auto px-4 py-10">
    {#each pages as page, index}
        <div class="snap-start shrink-0 card">
            <a href="/" class="card" on:click|preventDefault={() => handleClick(index)}>
                <img class="rounded-t-md h-96 object-cover object-top" src={`https://image.digitalcollections.manchester.ac.uk/iiif/${page.IIIFImageURL}/full/!348,348/0/default.jpg`} alt="" />
            </a>
            <br>
            <p class="text-center">Page {index + 1}</p>
        </div>
    {/each}
</div>
