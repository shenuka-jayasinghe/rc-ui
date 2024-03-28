<script lang="ts">
	import About from '$lib/About.svelte';
	import ImageViewer from '$lib/ImageViewer.svelte';
	import Tiles from '$lib/Tiles.svelte';
	import { TabGroup, Tab, TabAnchor } from '@skeletonlabs/skeleton';
	let tabSet: number = 0;
</script>

<div class="container mx-auto">
	<div class="border-4 border-indigo-500/100 grid grid-cols-2 gap-4">
		<div>
			<ImageViewer/>
		</div>
		<div>
			<TabGroup>
				<Tab bind:group={tabSet} name="tab1" value={0}>
					<svelte:fragment slot="lead"></svelte:fragment>
					<span>About</span>
				</Tab>
				<Tab bind:group={tabSet} name="tab2" value={1}>Contents</Tab>
				<Tab bind:group={tabSet} name="tab3" value={2}>Tiles</Tab>
				<!-- Tab Panels --->
				<svelte:fragment slot="panel">
					{#if tabSet === 0}
						<About />
					{:else if tabSet === 1}
						No manifests here
					{:else if tabSet === 2}
						<Tiles/>
					{/if}
				</svelte:fragment>
			</TabGroup>

		</div>
	</div>
</div>
