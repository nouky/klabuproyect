<script>
	import Button from './Button.svelte';
	import KwadrantSelect from './KwadrantSelect.svelte';
</script>

<!-- <div class="row align-top">
  <div class="row mb-2 m2">
    <div class="col row mr-2 m2 btn-previous-container">
      <button
        id="btn-previous"
        class="btn btn-dark mr-2 disabled btn-sheet"
      >
        Previous
      </button>
    </div>
    <div class="col row btn-next-container">
      <button id="btn-next" class="btn btn-dark disabled btn-sheet">
        Next
      </button>
    </div>
  </div>

  <div
    class="row mb-2 m2 simulate-stop-container"
    style="display: none"
  >
    <div class="col row mr-2 m2 btn-simulate-container">
      <button
        id="btn-simulate"
        class="btn btn-dark mr-2 disabled btn-sheet"
      >
        Simulate
      </button>
    </div>
    <div class="col row btn-stop-container">
      <button id="btn-stop" class="btn btn-dark disabled btn-sheet">
        Stop
      </button>
    </div>
  </div>

  <div class="row mb-2 btn-reset-container">
    <button id="btn-reset" class="btn btn-success disabled">
      Reset
    </button>
  </div>

  <div class="row mb-2 btn-outofrange-container d-none">
    <button
      id="btn-outofrange"
      class="btn btn-danger disabled"
      data-bs-toggle="modal"
      data-bs-target="#exampleModal"
    >
      Notes out of Range
    </button>
  </div>

  <div class="row mb-2 btn-change-container">
    <button id="btn-change" class="btn bg-orange disabled">
      Change Sheet
    </button>
  </div>

  <div class="row mb-3">
    <div class="col-3">
      <label for="loadSheet" class="form-label">Kwadrant</label>
    </div>
    <div class="col-9">
      <select
        id="selectKwadrant"
        class="form-select form-select-sm"
        aria-label=".form-select-sm example"
        disabled
      >
        <option value="1" selected="selected">
          Dansa, Fox, Polka i Tumba
        </option>
        <option value="2">Mazurka</option>
        <option value="3">Wals i Joropo</option>
      </select>
    </div>
  </div>
</div> -->

<div class="row align-top button-container">
	<div class="row">
		<Button _class="btn-previous-container" id="btn-previous" label="Previous" />
		<Button _class="btn-next-container" id="btn-next" label="Next" />
	</div>

	<div class="row simulate-stop-container" style="">
		<Button _class="btn-simulate-container" id="btn-simulate" label="Simulate" />
		<Button _class="btn-stop-container" id="btn-stop" label="Stop" />
	</div>

	<div class="row btn-reset-container">
		<Button btnclass="btn-success" id="btn-reset" label="Reset" />
	</div>

	<div class="row btn-outofrange-container d-none">
		<button
			id="btn-outofrange"
			class="btn btn-danger disabled"
			data-bs-toggle="modal"
			data-bs-target="#exampleModal"
		>
			Notes out of Range
		</button>
	</div>

	<div class="row btn-change-container">
		<button id="btn-change" class="btn bg-orange disabled"> Change Sheet </button>
	</div>

	<KwadrantSelect />
</div>
