# calculator.github.io

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Basic Calculator</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #667eea, #764ba2);
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    .calculator {
        background: #222;
        padding: 20px;
        border-radius: 15px;
        width: 300px;
        box-shadow: 0 10px 30px rgba(0,0,0,0.4);
    }

    .display {
        background: #000;
        color: #0f0;
        font-size: 2rem;
        padding: 15px;
        border-radius: 8px;
        text-align: right;
        margin-bottom: 15px;
        overflow-x: auto;
    }

    .buttons {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 10px;
    }

    button {
        padding: 18px;
        font-size: 1.2rem;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        background: #333;
        color: white;
        transition: 0.2s;
    }

    button:hover {
        background: #555;
    }

    .operator {
        background: #ff9500;
    }

    .operator:hover {
        background: #e08900;
    }

    .equal {
        background: #34c759;
        grid-column: span 2;
    }

    .equal:hover {
        background: #2ea94f;
    }

    .clear {
        background: #ff3b30;
    }

    .clear:hover {
        background: #e13228;
    }
</style>
</head>

<body>

<div class="calculator">
    <div class="display" id="display">0</div>

    <div class="buttons">
        <button class="clear" onclick="clearDisplay()">C</button>
        <button onclick="deleteLast()">⌫</button>
        <button class="operator" onclick="append('/')">÷</button>
        <button class="operator" onclick="append('*')">×</button>

        <button onclick="append('7')">7</button>
        <button onclick="append('8')">8</button>
        <button onclick="append('9')">9</button>
        <button class="operator" onclick="append('-')">−</button>

        <button onclick="append('4')">4</button>
        <button onclick="append('5')">5</button>
        <button onclick="append('6')">6</button>
        <button class="operator" onclick="append('+')">+</button>

        <button onclick="append('1')">1</button>
        <button onclick="append('2')">2</button>
        <button onclick="append('3')">3</button>
        <button class="equal" onclick="calculate()">=</button>

        <button onclick="append('0')">0</button>
        <button onclick="append('.')">.</button>
    </div>
</div>

<script>
    const display = document.getElementById("display");

    function append(value) {
        if (display.innerText === "0") {
            display.innerText = value;
        } else {
            display.innerText += value;
        }
    }

    function clearDisplay() {
        display.innerText = "0";
    }

    function deleteLast() {
        if (display.innerText.length === 1) {
            display.innerText = "0";
        } else {
            display.innerText = display.innerText.slice(0, -1);
        }
    }

    function calculate() {
        try {
            display.innerText = eval(display.innerText.replace("×", "*").replace("÷", "/"));
        } catch {
            display.innerText = "Error";
        }
    }

    // 🎹 Keyboard Support
    document.addEventListener("keydown", function(event) {
        if (!isNaN(event.key) || event.key === ".") {
            append(event.key);
        }
        if (["+", "-", "*", "/"].includes(event.key)) {
            append(event.key);
        }
        if (event.key === "Enter") {
            calculate();
        }
        if (event.key === "Backspace") {
            deleteLast();
        }
        if (event.key.toLowerCase() === "c") {
            clearDisplay();
        }
    });
</script>

</body>
</html>
