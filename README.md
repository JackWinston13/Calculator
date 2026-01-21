<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        body {
            font-family: 'DM Mono', monospace;
            background-color: #f4f4f4;
            display: grid;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        .grid-container {
            display: grid;
            align-items: center;
            justify-content: center;
        }
        .calculator-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-template-rows: repeat(6, 1fr);
            grid-gap: 1px;
            background-color: #999;
            padding: 5px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }
        textarea {
            grid-column: span 4;
            font-family: 'DM Mono', monospace;
            font-size: 25px;
            text-align: end;
            background-color: #fad3cb;
            padding: 15px;
            border: none;
            resize: none;
            border-radius: 5px 5px 0 0;
        }
        .calculator-grid button {
            font-family: 'DM Mono', monospace;
            font-size: 25px;
            background-color: #fff;
            border: none;
            cursor: pointer;
            transition: 0.2s;
        }
        .calculator-grid button:nth-child(n+18) {
            background-color: tomato;
            color: white;
        }
        button:hover,
        .calculator-grid button:nth-child(n+18):hover {
            background-color: #440b15;
            color: white;
        }
        @media (max-width: 480px) {
            .calculator-grid {
                width: 90vw;
                padding: 10px;
            }
            textarea, button {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="grid-container">
        <div class="calculator-grid">
            <textarea id="inputtext" placeholder="0" rows="1"></textarea>
            <button>C</button>
            <button>DEL</button>
            <button></button>
            <button>+</button>
            <button>7</button>
            <button>8</button>
            <button>9</button>
            <button>-</button>
            <button>4</button>
            <button>5</button>
            <button>6</button>
            <button>*</button>
            <button>1</button>
            <button>2</button>
            <button>3</button>
            <button>/</button>
            <button>0</button>
            <button>.</button>
            <button></button>
            <button>=</button>
        </div>
    </div>
    <script>
        const input = document.getElementById('inputtext');
        const buttons = document.querySelectorAll('button');

        function calculate(expression) {
            try {
                return new Function('return ' + expression)();
            } catch (error) {
                return 'Malformed Operation';
            }
        }

        function operation(buttonValue) {
            if (buttonValue === 'C') {
                input.value = '';
            } else if (buttonValue === 'DEL') {
                input.value = input.value.slice(0, -1);
            } else if (buttonValue === '=') {
                input.value = calculate(input.value);
            } else {
                input.value += buttonValue;
            }
        }

        buttons.forEach(button => {
            let buttonValue = button.innerText;
            button.addEventListener('click', function() {
                operation(buttonValue);
            });
        });
    </script>
</body>
</html>
