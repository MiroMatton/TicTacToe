<script>
  import Game from "./components/Game.svelte";
  import Start from "./components/Start.svelte";
  import Modal from "./components/Modal.svelte";
  let gameMode;
  let showModal = false;
  let winner;

  const toggleModal = () => {
    showModal = !showModal;
  };
</script>

<Modal {winner} bind:showModal bind:gameMode on:click={toggleModal} />
<div id="wrapper">
  {#if gameMode}
    <Game bind:winner bind:showModal bind:gameMode />
  {:else}
    <Start bind:gameMode />
  {/if}
</div>

<style lang="scss">
  @use "./assets/colors";

  #wrapper {
    width: 100%;
    max-width: 40rem;
    margin: 0 auto;
    overflow: auto;
    @media (min-width: colors.$mobile) {
      width: 100%;
    }
  }
</style>
