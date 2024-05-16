<script lang="ts">
	import * as OSMD from 'opensheetmusicdisplay';
	import NotesOutofRange from './NotesOutofRange.svelte';
	import SongXmlList from './SongXmlList.svelte';
	export let osmd: OSMD.OpenSheetMusicDisplay;
	export let isSheetLoaded;

	let sheetClass = isSheetLoaded ? 'active' : '';

	const onLoadSheet = (evt) => {
		let file = evt.target.files[0]; // FileList object

		if (!file.name.match('.*.xml') && !file.name.match('.*.musicxml')) {
			alert('You selected a non-xml file. Please select only music xml files.');
		} else {
			let reader = new FileReader();

			reader.onload = (e) => {
				osmd
					.load(e.target.result as string)
					.then(function () {
						osmd.render();
						osmd.cursor.show(); // this would show the cursor on the first note
						isSheetLoaded = true;
						sheetClass = 'active';
					})
					.catch((err) => {
						console.error(err);
					});
			};

			if (file.name.match('.*.mxl')) {
				// have to read as binary, otherwise JSZip will throw ("corrupted zip: missing 37 bytes" or similar)
				reader.readAsBinaryString(file);
			} else {
				reader.readAsText(file);
			}
		}
	};
</script>

{#if !isSheetLoaded}
	<NotesOutofRange />
	<div class="col-12 d-flex justify-content-center">
		<div id="inputfileContainer" class="col-6 mt-5">
			<label for="loadSheet" class="form-label">Select your XML Sheet</label>
			<input
				class="form-control form-control-sm"
				id="selectSheet"
				type="file"
				accept=".xml, .musicxml"
				on:change={onLoadSheet}
			/>
			<SongXmlList />
		</div>
	</div>
{/if}
<div id="sheetCanvas" class={sheetClass}></div>
