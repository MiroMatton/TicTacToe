<script>
  import X from "./X.svelte";
  import O from "./O.svelte";
  export let showModal;
  export let winner;
  let color = "";
  let message = "";

  $: if (showModal) {
    if (winner === X) (color = "lightBlue"), (message = "takes the round");
    else if (winner === O) (color = "yellow"), (message = "takes the round");
    else if (winner === "tie") (message = "Tie"), (color = "");
  }
</script>

{#if showModal}
  <div class="backdrop" on:click|self>
    <div class="modal">
      <h2>You Won!</h2>
      <div class="row">
        {#if winner != "tie"}
          <svelte:component this={winner} />
        {/if}
        <h1 class={color}>{message}</h1>
      </div>
      <div class="row">
        <button class="gray">quit</button><button class="yellow"
          >next round</button
        >
      </div>
    </div>
  </div>
{/if}

<style lang="scss">
  @use "../assets/colors";

  .backdrop {
    position: fixed;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    z-index: 100;
  }

  .modal {
    position: absolute;
    width: 100%;
    top: 25%;
    background-color: colors.$blue;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 4rem 0;

    h2 {
      color: colors.$gray;
      font-size: 2rem;
    }
  }

  h1 {
    color: colors.$gray;
    font-size: 4rem;
    padding-bottom: 0.5rem;
    &.lightBlue {
      color: colors.$lightBlue;
      margin-left: 3rem;
    }
    &.yellow {
      color: colors.$yellow;
    }
  }

  .row {
    display: flex;
    align-items: center;
  }
  button {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 1rem;
    box-shadow: 0 4px 0px 0px colors.$darkGray;
    border: none;
    margin: 1rem;
    background-color: colors.$gray;
    color: colors.$bg;
    padding: 0.5rem 1rem;
    cursor: pointer;
    font-size: 1.5rem;
    font-weight: bold;

    &.yellow {
      background-color: colors.$yellow;
      box-shadow: 0 4px 0px 0px colors.$darkYellow;
    }
  }
</style>
