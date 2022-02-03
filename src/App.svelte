<script>
  import IoMdRefresh from "svelte-icons/io/IoMdRefresh.svelte";
  import O from "./components/O.svelte";
  import X from "./components/X.svelte";

  let board = new Array(9).fill(null);
  let currentPlayer = X;

  const winCombos = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];

  const onClick = (i) => {
    if (board[i] !== X && board[i] !== O) board[i] = currentPlayer;

    currentPlayer = currentPlayer == X ? O : X;
    checkWinner();
  };

  const checkWinner = () => {
    if (!board.includes(null)) {
      alert("draw");
    } else {
      for (let i = 0; i < winCombos.length; i++) {
        if (
          equals3(
            board[winCombos[i][0]],
            board[winCombos[i][1]],
            board[winCombos[i][2]]
          )
        ) {
          alert("Winner: " + toString(board[winCombos[i][0]]));
        }
      }
    }
  };

  const equals3 = (a, b, c) => {
    return a == b && b == c && c != null;
  };

  const restart = () => {
    board = new Array(9).fill(null);
    currentPlayer = X;
  };

  const toString = (component) => {
    if (component === X) return "X";
    else return "Y";
  };
</script>

<div id="wrapper">
  <section id="header">
    <div class="icons">
      <O size={"small"} />
      <X size={"small"} />
    </div>
    <div class="turn">
      <svelte:component this={currentPlayer} size={"small"} color={"gray"} />
      <p>turn</p>
    </div>
    <div class="restart" on:click={() => restart()}>
      <div class="icon">
        <IoMdRefresh />
      </div>
    </div>
  </section>
  <section id="board">
    <div class="row">
      <div class="box" on:click={() => onClick(0)}>
        <svelte:component this={board[0]} />
      </div>
      <div class="box" on:click={() => onClick(1)}>
        <svelte:component this={board[1]} />
      </div>
      <div class="box" on:click={() => onClick(2)}>
        <svelte:component this={board[2]} />
      </div>
    </div>
    <div class="row">
      <div class="box" on:click={() => onClick(3)}>
        <svelte:component this={board[3]} />
      </div>
      <div class="box" on:click={() => onClick(4)}>
        <svelte:component this={board[4]} />
      </div>
      <div class="box" on:click={() => onClick(5)}>
        <svelte:component this={board[5]} />
      </div>
    </div>
    <div class="row">
      <div class="box" on:click={() => onClick(6)}>
        <svelte:component this={board[6]} />
      </div>
      <div class="box" on:click={() => onClick(7)}>
        <svelte:component this={board[7]} />
      </div>
      <div class="box" on:click={() => onClick(8)}>
        <svelte:component this={board[8]} />
      </div>
    </div>
  </section>
</div>

<style lang="scss">
  @use "./assets/colors";

  #wrapper {
    width: 100%;
    max-width: 40rem;
    margin: 0 auto;
    overflow: auto;
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
    background-color: colors.$blue;
    border-radius: 1rem;
    width: 10rem;
    margin: 1rem 0;
    box-shadow: 0 8px 0px 0px colors.$darkBlue;

    p {
      color: colors.$gray;
      font-size: 2rem;
      font-weight: bold;
      margin-left: 1rem;
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
    color: colors.$bg;
    width: 32px;
    height: 32px;
  }

  .restart {
    background-color: colors.$gray;
    padding: 1rem;
    margin: 1rem 1rem 1rem 0;
    border-radius: 1rem;
    box-shadow: 0 8px 0px 0px colors.$darkGray;
    cursor: pointer;
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
    box-shadow: 0 8px 0px 0px colors.$darkBlue;
    margin: 1rem;
    background-color: colors.$blue;
    cursor: pointer;
  }
</style>
