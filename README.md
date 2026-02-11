<!DOCTYPE html>
<html>
<head>
  <title>Test Support IA</title>
  <style>
    body { font-family: Arial; padding: 40px; }
    #chatbox {
      position: fixed;
      bottom: 20px;
      right: 20px;
      width: 300px;
      background: white;
      border: 1px solid #ccc;
      padding: 10px;
    }
    #messages {
      height: 200px;
      overflow: auto;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>

<h1>Mon entreprise test</h1>
<p>Bienvenue sur notre site.</p>

<div id="chatbox">
  <div id="messages"></div>
  <input type="text" id="userInput" placeholder="Votre message..." style="width:100%;" />
  <button onclick="sendMessage()">Envoyer</button>
</div>

<script>
async function sendMessage() {
  const input = document.getElementById("userInput");
  const message = input.value;
  if (!message) return;

  document.getElementById("messages").innerHTML += "<div><b>Vous:</b> " + message + "</div>";

  const response = await fetch("TON_WEBHOOK_N8N_ICI", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ message: message })
  });

  const data = await response.json();
  document.getElementById("messages").innerHTML += "<div><b>Bot:</b> " + data.reply + "</div>";

  input.value = "";
}
</script>

</body>
</html>

