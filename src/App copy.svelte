<script>
  import Modal from "./lib/components/Modal.svelte";
  import NoteContainer from "./lib/components/NoteContainer.svelte";

  let name = "Anouck";
  let lastname = "Noorden";
  let color = "black";
  let showModal = false;

  $: fullname = `${name} ${lastname}`;

  const toggleModal = () => {
    showModal = !showModal;
  };
</script>

<Modal isPromo={false} {showModal} on:click={toggleModal} />
<div class="card m-2 text-dark rounded-6 app-container">
  <NoteContainer />
</div>

<main>
  <h1>Test:{fullname}</h1>
  <input type="text" bind:value={name} />
  <input type="text" bind:value={lastname} />
  <input type="text" bind:value={color} />
  <button on:click={toggleModal}>Toggle Modal</button>
</main>

<style>
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
