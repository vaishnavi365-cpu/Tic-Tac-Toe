<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Tic Tac Toe</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color:white;
        }

        h1 {
            margin-top: 20px;
        }

        #status {
            font-size: 20px;
            margin: 15px;
            font-weight: bold;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 5px;
            justify-content: center;
            margin: 20px auto;
        }

        .cell {
            width: 100px;
            height: 100px;
            background-color:white;
            border: 2px solid #333;
            font-size: 40px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }

        .cell:hover {
            background-color:white;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>

<body>

    <h1>Tic Tac Toe</h1>
    <div id="status">Player X's Turn</div>

    <div class="board">
        <div class="cell" onclick="play(0)"></div>
        <div class="cell" onclick="play(1)"></div>
        <div class="cell" onclick="play(2)"></div>
        <div class="cell" onclick="play(3)"></div>
        <div class="cell" onclick="play(4)"></div>
        <div class="cell" onclick="play(5)"></div>
        <div class="cell" onclick="play(6)"></div>
        <div class="cell" onclick="play(7)"></div>
        <div class="cell" onclick="play(8)"></div>
    </div>

    <button onclick="restart()">Restart Game</button>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let gameOver = false;

        const statusText = document.getElementById("status");
        const cells = document.getElementsByClassName("cell");

        const winPatterns = [
            [0,1,2],
            [3,4,5],
            [6,7,8],
            [0,3,6],
            [1,4,7],
            [2,5,8],
            [0,4,8],
            [2,4,6]
        ];

        function play(index) {
            if (board[index] !== "" || gameOver) return;

            board[index] = currentPlayer;
            cells[index].innerText = currentPlayer;

            if (checkWinner()) {
                statusText.innerText = "Player " + currentPlayer + " Wins!";
                gameOver = true;
                return;
            }

            if (!board.includes("")) {
                statusText.innerText = "Game Draw!";
                gameOver = true;
                return;
            }

            currentPlayer = currentPlayer === "X" ? "O" : "X";
            statusText.innerText = "Player " + currentPlayer + "'s Turn";
        }

        function checkWinner() {
            for (let pattern of winPatterns) {
                let [a, b, c] = pattern;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    return true;
                }
            }
            return false;
        }

        function restart() {
            board = ["", "", "", "", "", "", "", "", ""];
            currentPlayer = "X";
            gameOver = false;
            statusText.innerText = "Player X's Turn";

            for (let cell of cells) {
                cell.innerText = "";
            }
        }
    </script>

</body>
</html>
