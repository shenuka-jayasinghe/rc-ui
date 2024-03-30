<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import { searchIcon } from '$lib/assets/search.js';

	// Highlight JS
	import hljs from 'highlight.js/lib/core';
	import 'highlight.js/styles/github-dark.css';
	import { storeHighlightJs } from '@skeletonlabs/skeleton';
	import xml from 'highlight.js/lib/languages/xml'; // for HTML
	import css from 'highlight.js/lib/languages/css';
	import javascript from 'highlight.js/lib/languages/javascript';
	import typescript from 'highlight.js/lib/languages/typescript';

	hljs.registerLanguage('xml', xml); // for HTML
	hljs.registerLanguage('css', css);
	hljs.registerLanguage('javascript', javascript);
	hljs.registerLanguage('typescript', typescript);
	storeHighlightJs.set(hljs);

	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';
	import { storePopup } from '@skeletonlabs/skeleton';
	import { assets } from '$app/paths';
	storePopup.set({ computePosition, autoUpdate, flip, shift, offset, arrow });
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<LightSwitch />
			<svelte:fragment slot="lead">
				<style>
					@import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');
					.text-xl.uppercase {
						font-family: 'Permanent Marker', cursive;
					}
				</style>
				<strong class="text-xl uppercase">R COLLECTIONS</strong>
			</svelte:fragment>

			<svelte:fragment slot="trail">
				<div class="input-group input-group-divider grid-cols-[auto_1fr_auto]">
					<input
						type="search"
						placeholder="Search..."
						class="box-border h-[30px] w-[200px] bg-gray-800"
					/>
					<button class="object-cover object-fit variant-filled h-[30px] w-[50px] bg-gray-800">
						<svg
							class="fill-purple-100 dark:fill-indigo-900"
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 -960 960 960"
							width="50"
							height="30"
						>
							{@html searchIcon}
						</svg>
					</button>
				</div>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
