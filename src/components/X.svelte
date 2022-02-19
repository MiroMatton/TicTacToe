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
  @use "sass:math";

  $width: 1.5rem;
  $height: 5rem;

  $widthSmall: 0.5rem;
  $heightSmall: 2rem;

  .X {
    .bar {
      width: $width;
      height: $height;
      background-color: colors.$lightBlue;
      border-radius: 0.2em;

      &:nth-child(1) {
        transform: translateY(math.div($height, 2)) rotate(45deg);
      }
      &:nth-child(2) {
        transform: translateY(math.div(-$height, 2)) rotate(-45deg);
      }

      &.winX {
        background-color: colors.$blue;
      }

      &.small {
        width: $widthSmall;
        height: $heightSmall;
        &:nth-child(1) {
          transform: translateY(math.div($heightSmall, 2)) rotate(45deg);
        }
        &:nth-child(2) {
          transform: translateY(math.div(-$heightSmall, 2)) rotate(-45deg);
        }

        &.gray {
          background-color: colors.$gray;
          margin-right: 0.5rem;
        }
      }
      @media (max-width: colors.$mobile) {
        width: $widthSmall;
        height: $heightSmall;
        &:nth-child(1) {
          transform: translateY(math.div($heightSmall, 2)) rotate(45deg);
        }
        &:nth-child(2) {
          transform: translateY(math.div(-$heightSmall, 2)) rotate(-45deg);
        }
      }
    }
  }
</style>
