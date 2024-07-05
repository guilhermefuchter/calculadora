# calculadora

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
        }
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .calculator {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }
        .display {
            width: 100%;
            padding: 10px;
            font-size: 2em;
            text-align: right;
            margin-bottom: 10px;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        button {
            padding: 20px;
            font-size: 1.2em;
            border: none;
            background-color: #e0e0e0;
            cursor: pointer;
            border-radius: 5px;
        }
        button:hover {
            background-color: #d4d4d4;
        }
        .equal {
            grid-column: span 2;
            background-color: #4CAF50;
            color: white;
        }
        .history {
            max-width: 400px;
            width: 100%;
            background-color: #fff;
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .history table {
            width: 100%;
            border-collapse: collapse;
        }
        .history th, .history td {
            padding: 10px;
            border: 1px solid #ddd;
            text-align: left;
        }
        .history th {
            background-color: #f4f4f4;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="calculator">
            <input type="text" class="display" id="display" disabled>
            <div class="buttons">
                <button onclick="clearDisplay()">C</button>
                <button onclick="deleteLast()">←</button>
                <button onclick="appendCharacter('%')">%</button>
                <button onclick="appendCharacter('/')">/</button>
                <button onclick="appendCharacter('7')">7</button>
                <button onclick="appendCharacter('8')">8</button>
                <button onclick="appendCharacter('9')">9</button>
                <button onclick="appendCharacter('*')">*</button>
                <button onclick="appendCharacter('4')">4</button>
                <button onclick="appendCharacter('5')">5</button>
                <button onclick="appendCharacter('6')">6</button>
                <button onclick="appendCharacter('-')">-</button>
                <button onclick="appendCharacter('1')">1</button>
                <button onclick="appendCharacter('2')">2</button>
                <button onclick="appendCharacter('3')">3</button>
                <button onclick="appendCharacter('+')">+</button>
                <button onclick="appendCharacter('0')">0</button>
                <button onclick="appendCharacter('.')">.</button>
                <button onclick="calculateResult()" class="equal">=</button>
            </div>
        </div>
        <div class="history">
            <h2>Histórico</h2>
            <table id="historyTable">
                <thead>
                    <tr>
                        <th>Expressão</th>
                        <th>Resultado</th>
                    </tr>
                </thead>
                <tbody id="historyBody"></tbody>
            </table>
        </div>
    </div>
    <script>
        let display = document.getElementById('display');
        let historyBody = document.getElementById('historyBody');   //declarando as variaveis

        function appendCharacter(char) {              // Adiciona um caractere ao visor.//
            display.value += char;
        }

        function clearDisplay() {                         //   Limpa o visor.
            display.value = '';
        }

        function deleteLast() {                               //  Remove o último caractere do visor.
            display.value = display.value.slice(0, -1);
        }

        function calculateResult() {                              // Avalia a expressão no visor e exibe o resultado.
            try {
                let result = eval(display.value);
                addToHistory(display.value, result);
                display.value = result;
            } catch (error) {
                display.value = 'Erro';
            }
        }

        function addToHistory(expression, result) {                  //  Adiciona a expressão e o resultado ao histórico.
            let row = document.createElement('tr');
            row.innerHTML = `<td onclick="useHistory('${expression}')">${expression}</td><td onclick="useHistory('${result}')">${result}</td>`;
            historyBody.appendChild(row);
        }

        function useHistory(value) {                         //Coloca um valor do histórico no visor.
            display.value = value;
        }

        document.addEventListener('DOMContentLoaded', () => {
            clearDisplay();
        });
    </script>
</body>
</html>
