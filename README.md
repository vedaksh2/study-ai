<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AI Study Helper powered by vedaksh</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.11.1/math.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      color: #222;
      padding: 20px;
      line-height: 1.6;
      transition: background 0.3s, color 0.3s;
    }

    body.dark {
      background: #121212;
      color: #e0e0e0;
    }

    h1, h2 {
      color: inherit;
    }

    button {
      margin: 5px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }

    textarea, input {
      width: 100%;
      margin-top: 10px;
      padding: 10px;
      font-size: 15px;
      box-sizing: border-box;
      border: 1px solid #ccc;
    }

    .section {
      margin-bottom: 30px;
    }

    textarea {
      height: 180px;
      background-color: #fff;
    }

    input {
      height: 40px;
    }

    body.dark textarea, body.dark input {
      background: #1e1e1e;
      color: #e0e0e0;
      border: 1px solid #444;
    }

    .voice-btn {
      background-color: #009688;
      color: white;
    }

    .dark-toggle {
      float: right;
      margin: 0;
    }

    a.youtube-link {
      display: inline-block;
      margin-top: 10px;
      color: #d9230f;
      font-weight: bold;
      text-decoration: none;
    }

    a.youtube-link:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>

  <h1>🧠 AI Study Helper powered by vedaksh 2
    <button class="dark-toggle" onclick="toggleDarkMode()">🌙 Toggle Dark Mode</button>
  </h1>

  <!-- Math Solver -->
  <div class="section">
    <h2>1️⃣ Math Equation Solver</h2>
    <input type="text" id="mathInput" placeholder="Enter math expression (e.g., 5*(2+3))">
    <button onclick="solveMath()">Solve</button>
    <textarea id="mathOutput" readonly placeholder="Math result will appear here..."></textarea>
  </div>

  <!-- Google Search + Voice -->
  <div class="section">
    <h2>2️⃣ Ask Anything (Google)</h2>
    <input type="text" id="googleInput" placeholder="Ask a question (e.g., What is gravity?)">
    <button onclick="googleIt()">Search on Google</button>
    <button class="voice-btn" onclick="startVoice()">🎤 Speak</button>
  </div>

  <!-- YouTube Link Section -->
  <div class="section">
    <h2>🎥 Visit Our YouTube Channel</h2>
    <a class="youtube-link" href="https://www.youtube.com/@vedaksh2-s2f" target="_blank">📺 youtube.com/@vedaksh2-s2f</a>
  </div>

  <script>
    // Solve Math
    function solveMath() {
      const input = document.getElementById('mathInput').value;
      try {
        const result = math.evaluate(input);
        document.getElementById('mathOutput').value = "Result: " + result;
      } catch (e) {
        document.getElementById('mathOutput').value = "Error: Invalid expression";
      }
    }

    // Google Search
    function googleIt() {
      const query = document.getElementById('googleInput').value;
      if (query.trim() !== "") {
        const url = "https://www.google.com/search?q=" + encodeURIComponent(query);
        window.open(url, "_blank");
      }
    }

    // Voice Recognition (Web Speech API)
    function startVoice() {
      if (!('webkitSpeechRecognition' in window)) {
        alert("Sorry, your browser doesn't support speech recognition.");
        return;
      }

      const recognition = new webkitSpeechRecognition();
      recognition.lang = "en-US";
      recognition.interimResults = false;
      recognition.maxAlternatives = 1;

      recognition.onstart = () => {
        document.getElementById("googleInput").placeholder = "Listening...";
      };

      recognition.onresult = (event) => {
        const transcript = event.results[0][0].transcript;
        document.getElementById("googleInput").value = transcript;
        document.getElementById("googleInput").placeholder = "Ask a question...";
      };

      recognition.onerror = (event) => {
        document.getElementById("googleInput").placeholder = "Ask a question...";
        alert("Error with speech recognition: " + event.error);
      };

      recognition.start();
    }

    // Dark Mode Toggle
    function toggleDarkMode() {
      document.body.classList.toggle('dark');
    }
  </script>

</body>
</html>

