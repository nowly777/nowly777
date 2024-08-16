<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
        }
        .cell {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100px;
            height: 100px;
            background-color: #fff;
            font-size: 2em;
            text-align: center;
            cursor: pointer;
            border: 1px solid #ccc;
        }
        .cell:hover {
            background-color: #eee;
        }
    </style>
</head>
<body>
    <div id="board" class="board">
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
        <div class="cell" onclick="makeMove(this)"></div>
    </div>
    <script>
        let currentPlayer = 'X';
        
        function checkWinner() {
            const cells = Array.from(document.querySelectorAll('.cell'));
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Horizontais
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Verticais
                [0, 4, 8], [2, 4, 6]             // Diagonais
            ];
            
            for (let pattern of winPatterns) {
                const [a, b, c] = pattern;
                if (cells[a].textContent && cells[a].textContent === cells[b].textContent && cells[a].textContent === cells[c].textContent) {
                    return cells[a].textContent;
                }
            }
            
            if (cells.every(cell => cell.textContent)) {
                return 'Empate';
            }
            
            return null;
        }
        
        function makeMove(cell) {
            if (cell.textContent) return; // Celula já preenchida
            
            cell.textContent = currentPlayer;
            const winner = checkWinner();
            
            if (winner) {
                setTimeout(() => alert(winner === 'Empate' ? 'Empate!' : `Jogador ${winner} venceu!`), 10);
                document.querySelectorAll('.cell').forEach(c => c.textContent = ''); // Limpa o tabuleiro
                currentPlayer = 'X';
            } else {
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            }
        }
    </script>
</body>
</html>
