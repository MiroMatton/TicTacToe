<script>
  export let size = "";
  export let color = "";
</script>

<div class="O {size} {color}" />

<style lang="scss">
  @use "../assets/colors";
  .O {
    width: 5rem;
    height: 5rem;
    border: 1.5rem solid colors.$yellow;
    border-radius: 100%;
    margin: 1rem;

    &.small {
      width: 2rem;
      height: 2rem;
      border: 0.5rem solid colors.$yellow;
      margin: 1rem;

      &.gray {
        border: 0.5rem solid colors.$gray;
        margin: 0rem;
      }
    }

    @media (max-width: colors.$mobile) {
      width: 2.5rem;
      height: 2.5rem;
      border: 0.75rem solid colors.$yellow;
    }
  }
</style>
