<template>
    <h1 class="game-title">Tic Tac Toe</h1>
    <p>{{ status }}</p>
    <div class="board">
        <Square v-for="(value, i) in squares" :key="i" :value="value" @square-click="clickSquare(i)" />
    </div>

    <button class="reset-button" @click="resetGame">Reset Game</button>
</template>
  
<script>
import Square from './Square.vue'

function calculateWinner(squares) {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
    ];
    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
            return squares[a];
        }
    }
    return null;
}

export default {
    name: 'Board',
    components: {
        Square
    },
    data() {
        return {
            squares: Array(9).fill(null),
            xIsNext: true,
        }
    },
    methods: {
        clickSquare(i) {
            const squares = this.squares.slice();
            if (squares[i] || calculateWinner(squares)) {
                return;
            }
            squares[i] = this.xIsNext ? 'X' : 'O';
            this.squares = squares;
            this.xIsNext = !this.xIsNext;
        },
        resetGame() {
            this.squares = Array(9).fill(null);
            this.xIsNext = true;
        },
    },
    computed: {
        status() {
            const winner = calculateWinner(this.squares);
            if (winner) {
                return 'Winner: ' + winner;
            } else {
                return 'Next player: ' + (this.xIsNext ? 'X' : 'O');
            }
        },
    },
}
</script>
  
<style scoped>
.board {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    height: 60vh;
    width: 60vh;
    margin: auto;
}

.reset-button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 16px;
  color: white;
  background-color: #007BFF;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.reset-button:hover {
  background-color: #0056b3;
}

.game-title {
  text-align: center;
  font-size: 3em;
  color: #007BFF;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  margin-bottom: 20px;
  font-family: 'Courier New', Courier, monospace;
  letter-spacing: 2px;
  text-transform: uppercase;
}
</style>