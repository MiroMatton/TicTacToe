<script>
  export let size = "";
  export let color = "";
</script>

<div class="X">
  <div class="bar {size} {color}" />
  <div class="bar {size} {color}" />
</div>

<style lang="scss">
  @use "../assets/colors";

  .X {
    .bar {
      width: 1.5rem;
      height: 5rem;
      background-color: colors.$lightBlue;
      border-radius: 0.2em;

      &:nth-child(1) {
        transform: translateY(2.5rem) rotate(45deg);
      }
      &:nth-child(2) {
        transform: translateY(-2.5rem) rotate(-45deg);
      }

      &.small {
        width: 0.5rem;
        height: 2rem;

        &:nth-child(1) {
          transform: translateY(1rem) rotate(45deg);
        }
        &:nth-child(2) {
          transform: translateY(-1rem) rotate(-45deg);
        }

        &.gray {
          background-color: colors.$gray;
        }
      }
    }
  }
</style>
