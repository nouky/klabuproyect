<script lang="ts">
	import * as OSMD from 'opensheetmusicdisplay';

	// import SheetViewer from './Sheet/sheetViewer.svelte';
	import SheetSection from './Sheet/SheetSection.svelte';

	export let osmd: OSMD.OpenSheetMusicDisplay;
	let isSheetLoaded = false;
</script>

<div class="col-9 align-self-start sheet-section">
	<SheetSection {osmd} bind:isSheetLoaded />
</div>
