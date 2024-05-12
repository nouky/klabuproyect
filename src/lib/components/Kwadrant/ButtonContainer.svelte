<script>
  import Button from "./Button.svelte";
  import KwadrantSelect from "./KwadrantSelect.svelte";
</script>

<div class="row align-top">
  <div class="row mb-1">
    <Button
      _class="btn-previous-container"
      id="btn-previous"
      label="Previous"
    />
    <Button _class="btn-next-container" id="btn-next" label="Next" />
  </div>

  <div class="row mb-1 simulate-stop-container" style="">
    <Button
      _class="btn-simulate-container"
      id="btn-simulate"
      label="Simulate"
    />
    <Button _class="btn-stop-container" id="btn-stop" label="Stop" />
  </div>

  <div class="row mb-1 btn-reset-container">
    <Button btnclass="btn-success" id="btn-reset" label="Reset" />
  </div>

  <div class="row mb-1 btn-outofrange-container d-none">
    <button
      id="btn-outofrange"
      class="btn btn-danger disabled"
      data-bs-toggle="modal"
      data-bs-target="#exampleModal"
    >
      Notes out of Range
    </button>
  </div>

  <div class="row mb-1 btn-change-container">
    <button id="btn-change" class="btn bg-orange disabled">
      Change Sheet
    </button>
  </div>

  <KwadrantSelect />
</div>
