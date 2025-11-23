# Web-page made by me using HTML,CSS,JAVASCRIPT
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Page</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      font-family: Arial, sans-serif;
      background: url('authBg.png') no-repeat center center fixed;
      background-size: cover;
      position: relative;
    }

    body::before {
      content: "";
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.5);
      z-index: 0;
    }

    .quote-box, .welcome-box {
      position: absolute;
      top: 20px;
      padding: 15px 20px;
      background-color: rgba(0, 0, 0, 0.6);
      border: 2px solid #00ffff;
      border-radius: 10px;
      box-shadow: 0 0 10px #00ffff;
      z-index: 1;
      backdrop-filter: blur(3px);
    }

    .quote-box { left: 30px; }
    .welcome-box { right: 30px; }

    .quote-text, .welcome-text {
      font-size: 1.2rem;
      font-weight: bold;
      color: #ffffff;
      margin: 0;
      text-shadow: 0 0 5px #fff, 0 0 10px #00ffff;
      font-style: italic;
    }

    h1 {
      font-size: 3.5rem;
      font-weight: bold;
      text-align: center;
      animation: glow 2s infinite alternate;
      z-index: 1;
      color: white;
      margin-bottom: 20px;
    }

    .word1 { color: #007bff; }
    .word2 { color: #ff5733; }
    .word3 { color: #28a745; }
    .word4 { color: #e83e8c; }
    .word5 { color: #ffc107; }

    @keyframes glow {
      0% { text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #f44606; }
      50% { text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffcc, 0 0 30px #ff00ff; }
      100% { text-shadow: 0 0 15px #ffcc00, 0 0 25px #ff6600, 0 0 35px #33ff00; }
    }

    .input-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 30px;
      z-index: 1;
      margin-top: 20px;
    }

    .center-box {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .side-gif {
      width: 100px;
      height: auto;
      cursor: pointer;
      transition: transform 0.3s ease;
      z-index: 1;
    }

    .side-gif:hover {
      transform: scale(1.1);
    }

    .textarea-box {
      width: 600px;
      max-width: 90%;
      height: 120px;
      padding: 15px;
      font-size: 1.2rem;
      border: 2px solid #00ffff;
      border-radius: 8px;
      z-index: 1;
      background-color: transparent;
      color: #ffffff;
      box-shadow: 0 0 10px #00ffff;
      resize: none;
      margin-bottom: 10px;
      backdrop-filter: blur(2px);
    }

    .textarea-box::placeholder {
      color: #ffffffcc;
    }

    .input-label {
      font-size: 1rem;
      color: #ffffff;
      font-weight: bold;
      z-index: 1;
      margin-bottom: 10px;
    }

    .mic-button, .google-button {
      padding: 10px 20px;
      font-size: 1rem;
      font-weight: bold;
      color: #fff;
      background-color: #007bff;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      z-index: 1;
      box-shadow: 0 0 10px #00ffff;
      transition: background-color 0.3s;
      margin-top: 10px;
    }

    .mic-button:hover, .google-button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <div class="quote-box">
    <p class="quote-text">You can feel free to talk with us...<br>We may help you with our best(Ayush Yadav).</p>
  </div>

  <div class="welcome-box">
    <p class="welcome-text">Welcome to your page</p>
  </div>

  <h1>
    <span class="word1">HOW</span>
    <span class="word2">CAN</span>
    <span class="word3">I</span>
    <span class="word4">HELP</span>
    <span class="word5">YOU?</span>
  </h1>

  <div class="input-wrapper">
    <img src="NN.png" alt="Left Assistant" class="side-gif" onclick="startVoice()">

    <div class="center-box">
      <textarea id="voiceInput" class="textarea-box" placeholder="Write your problem here..."></textarea>
      <div class="input-label">Type over here</div>
      <button class="mic-button" onclick="startVoice()">🎤 Speak</button>
      <button class="google-button" onclick="searchGoogle()">🔍 Google Search</button>
    </div>

    <img src="NN.png" alt="Right Assistant" class="side-gif" onclick="startVoice()">
  </div>

  <script>
    function startVoice() {
      const textarea = document.getElementById("voiceInput");
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = "en-IN";
      recognition.interimResults = false;
      recognition.maxAlternatives = 1;

      recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript;
        textarea.value += transcript + " ";
      };

      recognition.onerror = function(event) {
        alert("Voice recognition error: " + event.error);
      };

      recognition.start();
    }

    function searchGoogle() {
      const query = document.getElementById("voiceInput").value;
      if (query.trim() !== "") {
        const googleURL = "https://www.google.com/search?q=" + encodeURIComponent(query);
        window.open(googleURL, "_blank");
      } else {
        alert("Please enter a query before searching.");
      }
    }
  </script>
</body>
</html>
