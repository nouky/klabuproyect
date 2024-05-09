<script>
  export let strings;
  export let type;

  import { noteType } from "./Functions.svelte";

  strings = strings.filter((s) => s.inrange && s.type === type);
</script>

<div class="row justify-content-center text-secondary font-weight-bold">
  {noteType(type).label}
</div>
<div
  id="btn-{noteType(type).class}-container"
  class="row text-white note-label-container"
>
  {#each strings as note (note.position)}
    <div id={note.id} class="col waya {noteType(note.type).class}">
      {note.label.note}<sub>{note.label.octave}</sub>
    </div>
  {/each}
</div>
