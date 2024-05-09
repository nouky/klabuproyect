<script>
  // import Modal from "./lib/components/Modal.svelte";
  import NoteContainer from "./lib/components/NoteContainer.svelte";
  import KwadrantContainer from "./lib/components/KwadrantContainer.svelte";
  import SheetContainer from "./lib/components/SheetContainer.svelte";

  let showModal = false;

  const toggleModal = () => {
    showModal = !showModal;
  };
</script>

<main>
  <!-- <Modal isPromo={false} {showModal} on:click={toggleModal} /> -->
  <div class="card m-2 text-dark rounded-6 app-container">
    <NoteContainer />
    <div
      class="justify-content-center row align-items-center m-2 mb-0 text-secondary"
    >
      <KwadrantContainer />
      <SheetContainer />
    </div>
  </div>
</main>

<style>
</style>
