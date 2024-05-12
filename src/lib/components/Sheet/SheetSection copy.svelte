<script lang="ts">
  import { onDestroy, onMount } from "svelte";
  import SongXmlList from "./SongXmlList.svelte";
  import * as OSMD from "opensheetmusicdisplay";

  const { OpenSheetMusicDisplay } = OSMD;
  let osmd: OSMD.OpenSheetMusicDisplay;
  let isSheetLoaded = false;

  onMount(() => {
    osmd = new OpenSheetMusicDisplay("sheetCanvas", {
      // set options here
      backend: "svg",
      darkMode: false,
      drawFromMeasureNumber: 1,
      drawUpToMeasureNumber: Number.MAX_SAFE_INTEGER,
      cursorsOptions: [
        {
          type: 0,
          color: "red",
          alpha: 0.5,
          follow: true,
        },
      ],
    });
  });
  onDestroy(() => {
    osmd = undefined;
  });

  const OnLoadSheetFile = (evt) => {
    let file = evt.target.files[0]; // FileList object

    if (!file.name.match(".*.xml") && !file.name.match(".*.musicxml")) {
      alert("You selected a non-xml file. Please select only music xml files.");
    } else {
      let reader = new FileReader();

      reader.onload = (e) => {
        osmd
          .load(e.target.result as string)
          .then(function () {
            // get all notes in sheet
            let notesPerStaffPerMeasure = osmd.GraphicSheet.MeasureList.map(
              (stavesPerMeasure) =>
                stavesPerMeasure.map((staff) =>
                  staff.staffEntries.map((x) => ({
                    pitch: x.graphicalVoiceEntries[0].notes[0].ToStringShortGet,
                    value:
                      x.graphicalVoiceEntries[0].notes[0].graphicalNoteLength,
                    sum: null,
                  }))
                )
            );

            notesPerStaffPerMeasure.map((measure) =>
              measure.map((staff) =>
                staff.map((notes, index) => {
                  if (index == 0) {
                    notes.sum = notes.value;
                  } else {
                    notes.sum = OSMD.Fraction.plus(
                      staff[index - 1].sum,
                      notes.value
                    );
                  }
                  // notes = notes.sum;
                })
              )
            );
            console.log("NSpM:", notesPerStaffPerMeasure);

            notesPerStaffPerMeasure = notesPerStaffPerMeasure.map((measure) =>
              measure.map((staff) => new Array(...new Set(staff)))
            );

            // create sum of notes
            let noteSumPerStaffPerMeasure = notesPerStaffPerMeasure.map(
              (measure) =>
                measure.map((staff) =>
                  staff.map((note) => note.sum.realValue as number)
                )
            );

            // combine all staffs into 1 per measure and sort acending
            let noteTimelinePerMeasure = noteSumPerStaffPerMeasure.map(
              (measure) => new Array(...new Set(measure.flat())).sort()
            ) as number[][];
            console.log("mt:", noteTimelinePerMeasure);

            // create the note timeline for whole sheet
            let noteTimeline = noteTimelinePerMeasure.flatMap(
              (measure, index) =>
                measure.map((point) => (point = point + index * measure.last()))
            );
            console.log("ft:", noteTimeline);
            noteTimeline.unshift(0);

            osmd.render();
            osmd.cursor.show(); // this would show the cursor on the first note
          })
          .catch((err) => {
            console.error(err);
          });
      };

      if (file.name.match(".*.mxl")) {
        // have to read as binary, otherwise JSZip will throw ("corrupted zip: missing 37 bytes" or similar)
        reader.readAsBinaryString(file);
      } else {
        reader.readAsText(file);
      }
    }
  };
</script>

<div class="col-12 d-flex justify-content-center">
  <div id="inputfileContainer" class="col-6 mt-5">
    <label for="loadSheet" class="form-label">Select your XML Sheet</label>
    <input
      class="form-control form-control-sm"
      id="selectSheet"
      type="file"
      accept=".xml, .musicxml"
      on:change={OnLoadSheetFile}
    />
    <SongXmlList />
  </div>
</div>
<div id="sheetCanvas"></div>
