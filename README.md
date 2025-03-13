# tetris-test
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tetris</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #222;
        }
        canvas {
            border: 2px solid white;
        }
    </style>
</head>
<body>
    <canvas id="tetris" width="300" height="600"></canvas>
    <script>
        const canvas = document.getElementById("tetris");
        const ctx = canvas.getContext("2d");
        const ROWS = 20;
        const COLS = 10;
        const SIZE = 30;
        const COLORS = ["red", "blue", "green", "yellow", "orange", "purple", "cyan"];

        let board = Array.from({ length: ROWS }, () => Array(COLS).fill(0));
        
        function drawBoard() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            for (let r = 0; r < ROWS; r++) {
                for (let c = 0; c < COLS; c++) {
                    if (board[r][c]) {
                        ctx.fillStyle = COLORS[board[r][c] - 1];
                        ctx.fillRect(c * SIZE, r * SIZE, SIZE, SIZE);
                        ctx.strokeRect(c * SIZE, r * SIZE, SIZE, SIZE);
                    }
                }
            }
        }

        function dropPiece() {
            let col = Math.floor(Math.random() * COLS);
            for (let row = 0; row < ROWS; row++) {
                if (board[row][col] === 0) {
                    board[row][col] = Math.floor(Math.random() * COLORS.length) + 1;
                    break;
                }
            }
            drawBoard();
        }

        setInterval(dropPiece, 500);
    </script>
</body>
</html>
