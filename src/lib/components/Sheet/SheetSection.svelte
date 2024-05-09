<script lang="ts">
  import SongXmlList from "./SongXmlList.svelte";
  import * as OSMD from "opensheetmusicdisplay";

  const { OpenSheetMusicDisplay } = OSMD;
  let osmd;
  let isSheetLoaded = false;

  const onLoadSheet = (evt) => {
    let file = evt.target.files[0]; // FileList object

    if (!file.name.match(".*.xml") && !file.name.match(".*.musicxml")) {
      alert("You selected a non-xml file. Please select only music xml files.");
    } else {
      let reader = new FileReader();

      reader.onload = (e) => {
        //https://github.com/opensheetmusicdisplay/opensheetmusicdisplay/blob/develop/src/OpenSheetMusicDisplay/OSMDOptions.ts

        // let osmd = new OpenSheetMusicDisplay("sheetCanvas", {
        //   // set options here
        //   backend: "svg",
        //   darkMode: false,
        //   drawFromMeasureNumber: 1,
        //   followCursor: true,
        //   drawUpToMeasureNumber: Number.MAX_SAFE_INTEGER, // draw all measures, up to the end of the sample
        // });

        osmd.load(e.target.result).then(() => {
          const denominator =
            osmd.Sheet.SheetPlaybackSetting.rhythm.Denominator;
          const numerator = osmd.Sheet.SheetPlaybackSetting.rhythm.Numerator;
          const measures = osmd.Sheet.SourceMeasures.length;

          console.log(denominator, numerator, measures);

          osmd.render();
          // osmd.cursor.show();
        });
      };
    }
  };
</script>

test1
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
<div id="sheetCanvas"></div>
