<script>
  import IoMdRefresh from "svelte-icons/io/IoMdRefresh.svelte";

  let container;

  const onClick = () => {
    const child = document.createElement("div");
    child.className = "O";
    container.appendChild(child);
  };
</script>

<div id="wrapper">
  <section id="header">
    <div class="icons">
      <div class="O small" />
      <div class="X">
        <div class="bar small" />
        <div class="bar small" />
      </div>
    </div>
    <div class="turn">
      <div class="X">
        <div class="bar gray" />
        <div class="bar gray" />
      </div>
      <p>turn</p>
    </div>
    <div class="restart">
      <div class="icon">
        <IoMdRefresh />
      </div>
    </div>
  </section>
  <section id="board">
    <div class="row">
      <div class="box"><div class="O" /></div>
      <div class="box" on:click|once={() => onClick()} bind:this={container} />
      <div class="box" />
    </div>
    <div class="row">
      <div class="box" />
      <div class="box" />
      <div class="box" />
    </div>
    <div class="row">
      <div class="box" />
      <div class="box" />
      <div class="box" />
    </div>
  </section>
</div>

<style lang="scss">
  $bg: #192a32;
  $lightBlue: #31c4be;
  $blue: #1f3540;
  $darkBlue: #0f202a;
  $darkGray: #728893;
  $gray: #a8bec9;
  $yellow: #f2b236;

  #wrapper {
    width: 100%;
    max-width: 40rem;
    margin: 0 auto;
    overflow: auto;
  }

  :global(.O) {
    width: 5rem;
    height: 5rem;
    border: 1.5rem solid $yellow;
    border-radius: 100%;
    margin: 1rem;

    &.small {
      width: 2rem;
      height: 2rem;
      border: 0.5rem solid $yellow;
      margin: 1rem 0rem 1rem 1rem;
    }
  }

  .X {
    margin-left: 1.5rem;
    .bar {
      width: 1.5rem;
      height: 5rem;
      background-color: $lightBlue;
      border-radius: 0.2em;

      &:nth-child(1) {
        transform: translateY(2.5rem) rotate(45deg);
      }
      &:nth-child(2) {
        transform: translateY(-2.5rem) rotate(-45deg);
      }

      &.gray {
        width: 0.5rem;
        height: 2rem;
        background-color: $gray;

        &:nth-child(1) {
          transform: translateY(1rem) rotate(45deg);
        }
        &:nth-child(2) {
          transform: translateY(-1rem) rotate(-45deg);
        }
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
      }
    }

    .bar:nth-child(1) {
      transform: translateY(2.5rem) rotate(45deg);
    }

    .bar:nth-child(2) {
      transform: translateY(-2.5rem) rotate(-45deg);
    }
  }

  .icons {
    display: flex;
    align-items: center;
    justify-content: left;
    margin: 1rem 0;
  }

  .turn {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: $blue;
    border-radius: 1rem;
    width: 10rem;
    margin: 1rem 0;
    box-shadow: 0 8px 0px 0px $darkBlue;

    p {
      color: $gray;
      font-size: 2rem;
      font-weight: bold;
      margin: 1rem;
      padding-bottom: 0.5rem;
    }
  }

  section {
    margin: 0 2rem;
  }

  #header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .icon {
    color: $bg;
    width: 32px;
    height: 32px;
  }

  .restart {
    background-color: $gray;
    padding: 1rem;
    margin: 1rem 1rem 1rem 0;
    border-radius: 1rem;
    box-shadow: 0 8px 0px 0px $darkGray;
  }

  .row {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .box {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 1rem;
    width: 10rem;
    height: 10rem;
    box-shadow: 0 8px 0px 0px $darkBlue;
    margin: 1rem;
    background-color: $blue;
    cursor: pointer;
  }
</style>
