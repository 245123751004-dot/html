<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Program - Code Editor</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', sans-serif;
    }

    body {
      background: #1e1e2e;
      color: #cdd6f4;
      height: 100vh;
      display: flex;
      flex-direction: column;
    }

    header {
      background: #11111b;
      padding: 15px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 2px solid #89b4fa;
    }

    h1 {
      font-size: 24px;
      color: #89b4fa;
    }

    .controls {
      display: flex;
      gap: 10px;
    }

    button {
      padding: 10px 20px;
      background: #89b4fa;
      color: #11111b;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
    }

    button:hover {
      background: #74c7ec;
    }

    .container {
      flex: 1;
      display: flex;
      overflow: hidden;
    }

    .editor {
      flex: 1;
      display: flex;
      flex-direction: column;
      border-right: 1px solid #313244;
    }

    .tabs {
      background: #181825;
      padding: 8px 15px;
      display: flex;
      gap: 5px;
    }

    .tab {
      padding: 8px 16px;
      background: #313244;
      border-radius: 4px 4px 0 0;
      cursor: pointer;
    }

    .tab.active {
      background: #1e1e2e;
      border-bottom: 3px solid #89b4fa;
    }

    textarea {
      flex: 1;
      background: #1e1e2e;
      color: #cdd6f4;
      border: none;
      padding: 20px;
      font-size: 16px;
      font-family: 'Consolas', monospace;
      resize: none;
      outline: none;
    }

    .output-panel {
      width: 40%;
      background: #11111b;
      display: flex;
      flex-direction: column;
    }

    .output-header {
      background: #181825;
      padding: 12px 20px;
      font-weight: bold;
      border-bottom: 1px solid #313244;
    }

    #output {
      flex: 1;
      padding: 20px;
      background: #1e1e2e;
      color: #a6e3a1;
      font-family: 'Consolas', monospace;
      overflow-y: auto;
      white-space: pre-wrap;
    }

    footer {
      background: #11111b;
      padding: 10px;
      text-align: center;
      font-size: 14px;
      color: #6e738d;
    }
  </style>
</head>
<body>

  <header>
    <h1>💻 My Program</h1>
    <div class="controls">
      <button onclick="runCode()">▶ Run</button>
      <button onclick="clearOutput()">Clear Output</button>
    </div>
  </header>

  <div class="container">
    <!-- Code Editor -->
    <div class="editor">
      <div class="tabs">
        <div class="tab active">index.html</div>
        <div class="tab">script.js</div>
        <div class="tab">style.css</div>
      </div>
      <textarea id="code" placeholder="Write your HTML, CSS, or JavaScript here...">
// Welcome to My Program
console.log("Hello World! 👋");
document.body.style.background = "#1e1e2e";
      </textarea>
    </div>

    <!-- Output Panel -->
    <div class="output-panel">
      <div class="output-header">Output Console</div>
      <div id="output"></div>
    </div>
  </div>

  <footer>
    Simple HTML Program / Mini Code Editor • Made with ❤️
  </footer>

  <script>
    function runCode() {
      const code = document.getElementById('code').value;
      const output = document.getElementById('output');
      
      output.innerHTML = ''; // Clear previous output
      
      try {
        // For JavaScript execution (basic)
        if (code.includes('console.log')) {
          const oldLog = console.log;
          console.log = function(message) {
            output.innerHTML += message + '<br>';
          };
          
          eval(code);
          
          console.log = oldLog; // Restore original console
        } else {
          output.innerHTML = "Code executed successfully!<br>";
        }
      } catch (error) {
        output.style.color = '#f38ba8';
        output.innerHTML = `Error: ${error.message}`;
      }
    }

    function clearOutput() {
      document.getElementById('output').innerHTML = '';
    }

    // Keyboard shortcut: Ctrl + Enter to run
    document.addEventListener('keydown', function(e) {
      if (e.ctrlKey && e.key === 'Enter') {
        runCode();
      }
    });
  </script>

</body>
</html>
