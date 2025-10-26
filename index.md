<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chat Input Example</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f7f8fa;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .chat-container {
      background: #fff;
      border: 1px solid #ddd;
      border-radius: 10px;
      width: 400px;
      padding: 16px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
      display: flex;
      flex-direction: column;
    }

    .chat-input-area {
      display: flex;
      border: 1px solid #ccc;
      border-radius: 20px;
      padding: 8px 12px;
      background: #f1f1f1;
    }

    .chat-input {
      flex: 1;
      border: none;
      background: transparent;
      outline: none;
      font-size: 16px;
      padding: 6px;
    }

    .send-button {
      background-color: #0078ff;
      border: none;
      color: white;
      border-radius: 50%;
      width: 36px;
      height: 36px;
      cursor: pointer;
      font-size: 16px;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background 0.2s;
    }

    .send-button:hover {
      background-color: #005fd1;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-input-area">
      <input type="text" id="chatInput" class="chat-input" placeholder="Type a message..." />
      <button class="send-button" id="sendBtn">➤</button>
    </div>
  </div>

  <script>
    const sendBtn = document.getElementById('sendBtn');
    const chatInput = document.getElementById('chatInput');

    sendBtn.addEventListener('click', () => {
      const message = chatInput.value.trim();
      if (message) {
        console.log(message);
        chatInput.value = '';
        const chatContainer = document.querySelector('.chat-container');
        chatContainer.style.display = 'none';
      } else {
        alert("Please enter a message first!");
      }
    });

    // Allow pressing Enter to send the message
    chatInput.addEventListener('keypress', (e) => {
      if (e.key === 'Enter') {
        sendBtn.click();
      }
    });
  </script>
</body>
</html>
