<script lang="ts">
	import * as OSMD from 'opensheetmusicdisplay';
	import SongXmlList from './SongXmlList.svelte';
	export let osmd: OSMD.OpenSheetMusicDisplay;
	export let isSheetLoaded;

	const OnLoadSheetFile = (evt) => {
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

<span id="measure-number" class="absolute"></span>
<div>
	<div id="sheetCanvas" class="bg-white max-h-[865px] overflow-auto"></div>
</div>

{#if !isSheetLoaded}
	<div class="justify-content-center">
		<label class="label">
			<span> Select your XML Sheet </span>
			<input
				class="input"
				id="selectSheet"
				type="file"
				accept=".xml, .musicxml"
				on:change={OnLoadSheetFile}
			/>
		</label>
		<SongXmlList />
	</div>
{/if}
