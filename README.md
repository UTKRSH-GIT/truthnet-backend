<!DOCTYPE html>
<html>
<head>
  <title>Scientific Calculator</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      margin-top: 20px;
      background: #000; /* Black background */
      color: white;
    }
    .calc {
      width: 340px;
      margin: auto;
      padding: 15px;
      border-radius: 15px;
      background: #1a1a1a; /* Dark gray for contrast */
      box-shadow: 0px 0px 15px orange;
    }
    #display {
      width: 100%;
      height: 50px;
      font-size: 22px;
      margin-bottom: 12px;
      text-align: right;
      padding: 8px;
      border: none;
      border-radius: 8px;
      background: #000;
      color: orange;
      box-shadow: inset 0px 0px 5px orange;
    }
    button {
      width: 70px;
      height: 45px;
      margin: 4px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      background: #333;
      color: white;
      transition: 0.2s;
    }
    button:hover {
      background: orange;
      color: black;
    }
    .equal {
      width: 145px;
      background: orange;
      color: black;
      font-weight: bold;
    }
    .clear {
      background: red;
      color: white;
    }
    .mode {
      background: #ff9800;
      color: black;
      font-weight: bold;
    }
    .func {
      background: #444;
      color: orange;
    }
  </style>
</head>
<body>
  <div class="calc">
    <input type="text" id="display" readonly>
    <br>

    <!-- Mode Switch -->
    <button class="mode" onclick="toggleMode()">Deg</button>
    <button onclick="appendValue('Math.PI')">π</button>
    <button onclick="appendValue('Math.E')">e</button>
    <button class="clear" onclick="clearDisplay()">C</button>
    <br>

    <!-- Scientific Functions -->
    <button class="func" onclick="appendFunc('sin')">sin</button>
    <button class="func" onclick="appendFunc('cos')">cos</button>
    <button class="func" onclick="appendFunc('tan')">tan</button>
    <button onclick="appendValue('/')">/</button>
    <br>

    <button class="func" onclick="appendFunc('log')">log</button>
    <button class="func" onclick="appendFunc('sqrt')">√</button>
    <button class="func" onclick="appendFunc('pow')">x^y</button>
    <button onclick="appendValue('*')">*</button>
    <br>

    <!-- Numbers -->
    <button onclick="appendValue('7')">7</button>
    <button onclick="appendValue('8')">8</button>
    <button onclick="appendValue('9')">9</button>
    <button onclick="appendValue('-')">-</button>
    <br>

    <button onclick="appendValue('4')">4</button>
    <button onclick="appendValue('5')">5</button>
    <button onclick="appendValue('6')">6</button>
    <button onclick="appendValue('+')">+</button>
    <br>

    <button onclick="appendValue('1')">1</button>
    <button onclick="appendValue('2')">2</button>
    <button onclick="appendValue('3')">3</button>
    <button onclick="appendValue('(')">(</button>
    <br>

    <button onclick="appendValue('0')">0</button>
    <button onclick="appendValue('.')">.</button>
    <button onclick="appendValue(')')">)</button>
    <button class="equal" onclick="calculate()">=</button>
  </div>

  <script>
    let display = document.getElementById("display");
    let mode = "DEG"; // Default mode

    function appendValue(val) {
      display.value += val;
    }

    function appendFunc(func) {
      if (func === "sin") display.value += "sin(";
      else if (func === "cos") display.value += "cos(";
      else if (func === "tan") display.value += "tan(";
      else if (func === "log") display.value += "log(";
      else if (func === "sqrt") display.value += "sqrt(";
      else if (func === "pow") display.value += "pow(";
    }

    function clearDisplay() {
      display.value = "";
    }

    function toggleMode() {
      if (mode === "DEG") {
        mode = "RAD";
        document.querySelector(".mode").innerText = "Rad";
      } else {
        mode = "DEG";
        document.querySelector(".mode").innerText = "Deg";
      }
    }

    function calculate() {
      try {
        let expr = display.value;

        // Replace functions with Math equivalents
        expr = expr.replace(/sin\(/g, "Math.sin(");
        expr = expr.replace(/cos\(/g, "Math.cos(");
        expr = expr.replace(/tan\(/g, "Math.tan(");
        expr = expr.replace(/log\(/g, "Math.log(");
        expr = expr.replace(/sqrt\(/g, "Math.sqrt(");
        expr = expr.replace(/pow\(/g, "Math.pow(");

        // Degree mode conversion
        if (mode === "DEG") {
          expr = expr.replace(/Math\.sin\(([^)]+)\)/g, "Math.sin(($1)*Math.PI/180)");
          expr = expr.replace(/Math\.cos\(([^)]+)\)/g, "Math.cos(($1)*Math.PI/180)");
          expr = expr.replace(/Math\.tan\(([^)]+)\)/g, "Math.tan(($1)*Math.PI/180)");
        }

        display.value = eval(expr);
      } catch {
        display.value = "Error";
      }
    }
  </script>
</body>
</html>
