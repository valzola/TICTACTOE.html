<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
        }
        table {
            border-collapse: collapse;
        }
        td {
            width: 100px;
            height: 100px;
            text-align: center;
            vertical-align: middle;
            font-size: 36px;
            border: 1px solid #000;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <table id="board">
        <tr>
            <td data-row="0" data-col="0"></td>
            <td data-row="0" data-col="1"></td>
            <td data-row="0" data-col="2"></td>
        </tr>
        <tr>
            <td data-row="1" data-col="0"></td>
            <td data-row="1" data-col="1"></td>
            <td data-row="1" data-col="2"></td>
        </tr>
        <tr>
            <td data-row="2" data-col="0"></td>
            <td data-row="2" data-col="1"></td>
            <td data-row="2" data-col="2"></td>
        </tr>
    </table>
    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const board = [
                ["", "", ""],
                ["", "", ""],
                ["", "", ""]
            ];
            const cells = document.querySelectorAll("td");

            function checkWinner(board, player) {
                const winConditions = [
                    [board[0][0], board[0][1], board[0][2]],
                    [board[1][0], board[1][1], board[1][2]],
                    [board[2][0], board[2][1], board[2][2]],
                    [board[0][0], board[1][0], board[2][0]],
                    [board[0][1], board[1][1], board[2][1]],
                    [board[0][2], board[1][2], board[2][2]],
                    [board[0][0], board[1][1], board[2][2]],
                    [board[0][2], board[1][1], board[2][0]]
                ];
                return winConditions.some(condition => condition.every(cell => cell === player));
            }

            function minimax(board, depth, isMaximizing) {
                if (checkWinner(board, "X")) return -10 + depth;
                if (checkWinner(board, "O")) return 10 - depth;
                if (board.flat().every(cell => cell)) return 0;

                if (isMaximizing) {
                    let maxEval = -Infinity;
                    for (let i = 0; i < 3; i++) {
                        for (let j = 0; j < 3; j++) {
                            if (!board[i][j]) {
                                board[i][j] = "O";
                                const eval = minimax(board, depth + 1, false);
                                board[i][j] = "";
                                maxEval = Math.max(maxEval, eval);
                            }
                        }
                    }
                    return maxEval;
                } else {
                    let minEval = Infinity;
                    for (let i = 0; i < 3; i++) {
                        for (let j = 0; j < 3; j++) {
                            if (!board[i][j]) {
                                board[i][j] = "X";
                                const eval = minimax(board, depth + 1, true);
                                board[i][j] = "";
                                minEval = Math.min(minEval, eval);
                            }
                        }
                    }
                    return minEval;
                }
            }

            function bestMove(board) {
                let bestEval = -Infinity;
                let move = null;
                for (let i = 0; i < 3; i++) {
                    for (let j = 0; j < 3; j++) {
                        if (!board[i][j]) {
                            board[i][j] = "O";
                            const eval = minimax(board, 0, false);
                            board[i][j] = "";
                            if (eval > bestEval) {
                                bestEval = eval;
                                move = { i, j };
                            }
                        }
                    }
                }
                return move;
            }

            function makeMove(row, col, player) {
                if (!board[row][col]) {
                    board[row][col] = player;
                    document.querySelector(`[data-row="${row}"][data-col="${col}"]`).innerText = player;
                    return true;
                }
                return false;
            }

            function handleClick(event) {
                const row = event.target.getAttribute("data-row");
                const col = event.target.getAttribute("data-col");
                if (makeMove(row, col, "X")) {
                    if (checkWinner(board, "X")) {
                        alert("Player X wins!");
                        resetBoard();
                    } else if (board.flat().every(cell => cell)) {
                        alert("It's a tie!");
                        resetBoard();
                    } else {
                        const aiMove = bestMove(board);
                        if (aiMove) {
                            makeMove(aiMove.i, aiMove.j, "O");
                            if (checkWinner(board, "O")) {
                                alert("Player O wins!");
                                resetBoard();
                            }
                        }
                    }
                }
            }

            function resetBoard() {
                board.forEach((row, i) => row.forEach((_, j) => board[i][j] = ""));
                cells.forEach(cell => cell.innerText = "");
            }

            cells.forEach(cell => cell.addEventListener("click", handleClick));
        });
    </script>
</body>
</html>
