<script>
  $: board = [" ", " ", " ", " ", " ", " ", " ", " ", " "];
  let winner = " ";
  let turn = "O";

  function play(pos) {
    if (board[pos] === " ") {
      turn = turn === "O" ? "X" : "O";
      board[pos] = board[pos] !== " " ? board[pos] : turn;
      winner = checkWinner(board);
    }
  }

  function resetBoard() {
    for (let pos in board) {
      board[pos] = " ";
    }
    winner = " ";
  }

  function checkWinner(_board) {
    let winner_pos = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ];

    for (let i = 0; i < winner_pos.length; i++) {
      const [a, b, c] = winner_pos[i];
      if (_board[a] && _board[a] === _board[b] && _board[a] === _board[c]) {
        return _board[a];
      }
    }

    if (_board.every(el => el !== " ")) {
      return "Empate";
    }
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 250px;
    margin: 0 auto;
  }

  table {
    border: 1px solid black;
    border-collapse: collapse;
  }

  tr {
    border: 1px solid black;
    margin: 0 auto;
  }

  td {
    border: 1px solid #ccc;
    margin: 0 auto;
    padding: 5px;
    height: 65px;
    width: 65px;
  }

  .tableButton {
    border: none;
    margin: 0 auto;
    text-align: center;
    font-size: 25px;
    height: 100%;
    width: 100%;
    background-color: white;
  }

  .resetButton {
    margin-top: 20px;
    background-color: #4caf50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
  }
</style>

<svelte:head>
  <title>Jogo da Velha</title>
</svelte:head>

<main>

  {#if winner !== ' '}
    <p>Vencedor: {winner}</p>
  {/if}

  <table>
    <tr>
      <td>
        <button class="tableButton" on:click={() => play(0)}>{board[0]}</button>
      </td>
      <td>
        <button class="tableButton" on:click={() => play(1)}>{board[1]}</button>
      </td>
      <td>
        <button class="tableButton" on:click={() => play(2)}>{board[2]}</button>
      </td>
    </tr>
    <tr>
      <td>
        <button class="tableButton" on:click={() => play(3)}>{board[3]}</button>
      </td>
      <td>
        <button class="tableButton" on:click={() => play(4)}>{board[4]}</button>
      </td>
      <td>
        <button class="tableButton" on:click={() => play(5)}>{board[5]}</button>
      </td>
    </tr>
    <tr>
      <td>
        <button class="tableButton" on:click={() => play(6)}>{board[6]}</button>
      </td>
      <td>
        <button class="tableButton" on:click={() => play(7)}>{board[7]}</button>
      </td>
      <td>
        <button class="tableButton" on:click={() => play(8)}>{board[8]}</button>
      </td>
    </tr>
  </table>

  <div class="container">
    <button class="resetButton" on:click={resetBoard}>RESET</button>
  </div>
</main>
