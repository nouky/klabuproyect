<script lang="ts">
	import { onDestroy, onMount } from 'svelte';
	import NoteContainer from '../lib/components/NoteContainer.svelte';
	import KwadrantContainer from '../lib/components/KwadrantContainer.svelte';
	import SheetContainer from '../lib/components/SheetContainer.svelte';
	import * as OSMD from 'opensheetmusicdisplay';

	const { OpenSheetMusicDisplay } = OSMD;
	let osmd: OSMD.OpenSheetMusicDisplay;
	let isSheetLoaded = false;

	onMount(() => {
		osmd = new OpenSheetMusicDisplay('sheetCanvas', {
			// set options here
			backend: 'svg',
			darkMode: false,
			drawFromMeasureNumber: 1,
			drawUpToMeasureNumber: Number.MAX_SAFE_INTEGER,
			cursorsOptions: [
				{
					type: 0,
					color: 'red',
					alpha: 0.5,
					follow: true
				}
			]
		});
	});
	onDestroy(() => {
		osmd = undefined;
	});
</script>

<NoteContainer />
<div class="justify-content-center row align-items-center m-2 mb-0 text-secondary">
	<KwadrantContainer />
	<SheetContainer {osmd} />
</div>
