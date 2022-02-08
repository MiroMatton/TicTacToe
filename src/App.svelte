<script>
  import IoMdRefresh from "svelte-icons/io/IoMdRefresh.svelte";
  import O from "./components/O.svelte";
  import X from "./components/X.svelte";
  import Modal from "./components/Modal.svelte";

  let board = new Array(9).fill(null);
  let currentPlayer = X;
  let winner;
  let showModal = false;
  let scoreX = 0,
    scoreO = 0,
    scoreDraw = 0;

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
    if (winner) return;
    if (board[i] !== X && board[i] !== O) board[i] = currentPlayer;

    currentPlayer = currentPlayer == X ? O : X;
    checkWinner();
  };

  const checkWinner = () => {
    if (!board.includes(null)) {
      score(winner);
      winner = null;
      showModal = true;
    } else {
      for (let i = 0; i < winCombos.length; i++) {
        if (
          equals3(
            board[winCombos[i][0]],
            board[winCombos[i][1]],
            board[winCombos[i][2]]
          )
        ) {
          winner = board[winCombos[i][0]];
          score(board[winCombos[i][0]]);
          showModal = true;
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
    winner = null;
  };

  const score = (winner) => {
    if (winner === X) scoreX++;
    else if (winner === O) scoreO++;
    else scoreDraw++;
  };

  const toggleModal = () => {
    showModal = !showModal;
  };
</script>

<Modal {showModal} {winner} on:click={toggleModal} />
<div id="wrapper">
  <section id="header">
    <div class="grid">
      <div class="icons">
        <O size={"small"} />
        <X size={"small"} />
      </div>
      <div class="box turn">
        <svelte:component this={currentPlayer} size={"small"} color={"gray"} />
        <p>turn</p>
      </div>
      <div class="container">
        <div class="restart" on:click={() => restart()}>
          <div class="icon">
            <IoMdRefresh />
          </div>
        </div>
      </div>
    </div>
  </section>
  <section id="board">
    <div class="grid">
      <div class="box" on:click={() => onClick(0)}>
        <svelte:component this={board[0]} />
      </div>
      <div class="box" on:click={() => onClick(1)}>
        <svelte:component this={board[1]} />
      </div>
      <div class="box" on:click={() => onClick(2)}>
        <svelte:component this={board[2]} />
      </div>
      <div class="box" on:click={() => onClick(3)}>
        <svelte:component this={board[3]} />
      </div>
      <div class="box" on:click={() => onClick(4)}>
        <svelte:component this={board[4]} />
      </div>
      <div class="box" on:click={() => onClick(5)}>
        <svelte:component this={board[5]} />
      </div>
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
  <section id="footer">
    <div class="grid">
      <div class="box score blue">
        <p>X (YOU)</p>
        <h2>{scoreX}</h2>
      </div>
      <div class="box score gray">
        <p>draw</p>
        <h2>{scoreDraw}</h2>
      </div>
      <div class="box score yellow">
        <p>O (CPU)</p>
        <h2>{scoreO}</h2>
      </div>
    </div>
  </section>
</div>

<style lang="scss">
  @use "./assets/colors";
  $mobile: 650px;

  #wrapper {
    width: 100%;
    max-width: 40rem;
    margin: 0 auto;
    overflow: auto;
    @media (min-width: $mobile) {
      width: 100%;
    }
  }

  .icons {
    display: flex;
    align-items: center;
    justify-content: left;
    margin: 1rem 0;
  }

  .icon {
    color: colors.$bg;
    width: 32px;
    height: 32px;
  }

  .container {
    display: flex;
    align-items: center;
    justify-content: flex-end;

    .restart {
      background-color: colors.$gray;
      padding: 1rem;
      border-radius: 1rem;
      margin-right: 1rem;
      box-shadow: 0 6px 0px 0px colors.$darkGray;
      cursor: pointer;
    }
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 0.5em;

    .box {
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 1rem;
      box-shadow: 0 8px 0px 0px colors.$darkBlue;
      margin: 1rem;
      background-color: colors.$blue;
      cursor: pointer;

      &::before {
        content: "";
        display: block;
        height: 0;
        width: 0;
        padding-top: 100%;
      }

      h2 {
        color: colors.$bg;
        font-size: 1.5rem;
        font-weight: bold;
      }

      &.turn {
        &::before {
          content: "";
          display: block;
          height: 0;
          width: 0;
          padding-top: 5%;
        }

        p {
          color: colors.$gray;
          font-size: 2rem;
          font-weight: bold;
          margin-left: 0.5rem;
          padding-bottom: 0.5rem;
        }
      }

      &.score {
        flex-direction: column;
        align-items: center;
        justify-content: center;
        color: colors.$bg;
        box-shadow: 0 0 0 0;
        cursor: auto;

        &::before {
          content: "";
          display: block;
          height: 0;
          width: 0;
          padding-top: 5%;
        }
        &.blue {
          background-color: colors.$lightBlue;
        }
        &.gray {
          background-color: colors.$gray;
        }
        &.yellow {
          background-color: colors.$yellow;
        }
      }
    }
  }
</style>
