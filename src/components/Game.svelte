<script context="module">
  let restart;
  export function modalRestart() {
    restart();
  }
</script>

<script>
  import IoMdRefresh from "svelte-icons/io/IoMdRefresh.svelte";
  import O from "./O.svelte";
  import X from "./X.svelte";
  import Logo from "./Logo.svelte";

  export let winner;
  export let showModal;
  export let gameMode;

  let board = new Array(9).fill(null);
  let winnerRow = new Array(9).fill("");
  let currentPlayer = X;
  let scoreX = 0,
    scoreO = 0,
    scoreDraw = 0;
  let human = X;
  let cpu = O;

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
    if (board[i] === X || board[i] === O) return;
    board[i] = human;
    gameOver(checkWinner());
    if (winner) return;
    CPU();
    gameOver(checkWinner());
  };

  const gameOver = (result) => {
    if (result === null) return;
    if (result === "tie") {
      winner = result;
      score(winner);
      showModal = true;
    } else {
      checkWinner(true);
      winner = result;
      score(result);
      showModal = true;
    }
  };

  const checkWinner = (end) => {
    for (let i = 0; i < winCombos.length; i++) {
      if (
        equals3(
          board[winCombos[i][0]],
          board[winCombos[i][1]],
          board[winCombos[i][2]]
        )
      ) {
        if (end) {
          winnerRow[winCombos[i][0]] =
            board[winCombos[i][0]] === X ? "winX" : "winO";
          winnerRow[winCombos[i][1]] =
            board[winCombos[i][1]] === X ? "winX" : "winO";
          winnerRow[winCombos[i][2]] =
            board[winCombos[i][2]] === X ? "winX" : "winO";
        }
        return board[winCombos[i][0]];
      }
    }
    if (!board.includes(null)) return "tie";
    return null;
  };

  const equals3 = (a, b, c) => {
    return a == b && b == c && c != null;
  };

  restart = () => {
    board = new Array(9).fill(null);
    winnerRow = new Array(9).fill("");
    currentPlayer = X;
    winner = null;
  };

  const score = (winner) => {
    if (winner === X) scoreX++;
    else if (winner === O) scoreO++;
    else scoreDraw++;
  };

  const CPUMoveImpossible = () => {
    currentPlayer = cpu;
    let bestScore = Infinity;
    let bestMove;
    for (let i = 0; i < board.length; i++) {
      if (board[i] !== null) continue; // if spot isn't available
      board[i] = cpu;
      let score = miniMax(board, 0, true);
      board[i] = null;
      if (score < bestScore) {
        bestScore = score;
        bestMove = i;
      }
    }
    board[bestMove] = cpu;
    currentPlayer = human;
  };

  const miniMax = (board, depth, isMaximizing) => {
    let result = checkWinner();
    if (result !== null) {
      if (result === X) return 10 - depth;
      else if (result === O) return -10 + depth;
      else return 0;
    }
    if (isMaximizing) {
      let bestScore = -Infinity;
      for (let i = 0; i < board.length; i++) {
        if (board[i] !== null) continue; // if spot isn't available
        board[i] = human;
        let score = miniMax(board, depth + 1, false);
        board[i] = null;
        bestScore = Math.max(score, bestScore);
      }
      return bestScore;
    } else {
      let bestScore = Infinity;
      for (let i = 0; i < board.length; i++) {
        if (board[i] !== null) continue; // if spot isn't available
        board[i] = cpu;
        let score = miniMax(board, depth + 1, true);
        board[i] = null;
        bestScore = Math.min(score, bestScore);
      }
      return bestScore;
    }
  };

  const CPUMoveEasy = (board) => {
    let i = Math.floor(Math.random() * 8) + 0;
    if (board[i] !== null || board[i] === X) CPUMoveEasy(board);
    else {
      board[i] = cpu;
    }
  };

  const CPU = () => {
    if (gameMode == "impossible") CPUMoveImpossible(board);
    else if (gameMode == "easy") CPUMoveEasy(board);
  };
</script>

<section id="header">
  <div class="grid">
    <Logo />
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
    <div class="box {winnerRow[0]}" on:click={() => onClick(0)}>
      <svelte:component this={board[0]} color={winnerRow[0]} />
    </div>
    <div class="box {winnerRow[1]}" on:click={() => onClick(1)}>
      <svelte:component this={board[1]} color={winnerRow[1]} />
    </div>
    <div class="box {winnerRow[2]}" on:click={() => onClick(2)}>
      <svelte:component this={board[2]} color={winnerRow[2]} />
    </div>
    <div class="box {winnerRow[3]}" on:click={() => onClick(3)}>
      <svelte:component this={board[3]} color={winnerRow[3]} />
    </div>
    <div class="box {winnerRow[4]}" on:click={() => onClick(4)}>
      <svelte:component this={board[4]} color={winnerRow[4]} />
    </div>
    <div class="box {winnerRow[5]}" on:click={() => onClick(5)}>
      <svelte:component this={board[5]} color={winnerRow[5]} />
    </div>
    <div class="box {winnerRow[6]}" on:click={() => onClick(6)}>
      <svelte:component this={board[6]} color={winnerRow[6]} />
    </div>
    <div class="box {winnerRow[7]}" on:click={() => onClick(7)}>
      <svelte:component this={board[7]} color={winnerRow[7]} />
    </div>
    <div class="box {winnerRow[8]}" on:click={() => onClick(8)}>
      <svelte:component this={board[8]} color={winnerRow[8]} />
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

<style lang="scss">
  @use "../assets/colors";
  $mobile: 650px;

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

      &.winX {
        background-color: colors.$lightBlue;
        box-shadow: 0 8px 0px 0px colors.$darkLightBlue;
      }

      &.winO {
        background-color: colors.$yellow;
        box-shadow: 0 8px 0px 0px colors.$darkYellow;
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
