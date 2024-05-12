<script>
  import strings from "../json/strings.json";
  import NoteType from "./NoteType.svelte";
</script>

<div class="justify-content-center row align-items-center m-2">
  <div class="col">
    <NoteType {strings} type="B" />
  </div>
  <div class="col-3">
    <NoteType {strings} type="A" />
  </div>
  <div class="col-8">
    <NoteType {strings} type="M" />
  </div>
</div>
