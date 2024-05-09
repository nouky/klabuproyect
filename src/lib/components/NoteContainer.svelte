<script>
  import strings from "../json/strings.json";
  import NoteDiv from "./NoteDiv.svelte";
</script>

<div class="justify-content-center row align-items-center m-2">
  <div class="col">
    <NoteDiv {strings} type="B" />
  </div>
  <div class="col-3">
    <NoteDiv {strings} type="A" />
  </div>
  <div class="col-8">
    <NoteDiv {strings} type="M" />
  </div>
</div>
