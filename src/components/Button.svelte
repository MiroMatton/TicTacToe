<script>
  export let color = "";
</script>

<button class={color} on:click><slot /></button>

<style lang="scss">
  @use "../assets/colors";
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
    &.lightBlue {
      background-color: colors.$lightBlue;
      box-shadow: 0 4px 0px 0px colors.$darkLightBlue;
    }
  }
</style>
