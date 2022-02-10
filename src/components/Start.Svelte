<script>
  import Logo from "./Logo.svelte";
  import Button from "./Button.svelte";
  export let gameMode;
</script>

<div class="center">
  <Logo />
  <div class="box">
    <h2>Pick your mark</h2>
  </div>
  <Button color={"lightBlue"} on:click={() => (gameMode = "easy")}
    >NEW GAME (EASY)</Button
  >
  <Button color={"yellow"} on:click={() => (gameMode = "impossible")}
    >NEW GAME (IMPOSSIBLE)</Button
  >
</div>

<style lang="scss">
  @use "../assets/colors";
  .center {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .box {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 1rem;
    box-shadow: 0 8px 0px 0px colors.$darkBlue;
    margin: 1rem;
    background-color: colors.$blue;
    padding: 1rem;

    h2 {
      color: colors.$gray;
      font-size: 1.5rem;
      font-weight: bold;
    }
  }
</style>
