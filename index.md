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

    /* --- CSS for Styling the Button --- */
    .send-message-button {
      /* Background and Dimensions */
      background-color: #00008b; /* A deep blue, similar to the image */
      color: white; /* White text */
      padding: 15px 30px; /* Padding for height and width */
      font-size: 18px; /* Readable text size */
      font-weight: bold;
      cursor: pointer; /* Changes mouse to a pointer on hover */
      border: none; /* Remove default button border */
      display: inline-block; /* Allows setting padding/margin */
      text-align: center;
      border-radius: 5px; /* Slight rounding of corners */
  
      /* The White Border/Outline Effect */
      box-shadow: 0 0 0 2px white; /* A 2px white "stroke" */
      outline: 2px solid #00008b; /* Helps create the gap/depth effect */
    }
  
    .send-message-button:hover {
      background-color: #0000a0; /* Slightly lighter blue on hover */
    }
  </style>

  <script type="text/javascript">
    function initEmbeddedMessaging() {
      try {
        embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'

        // Hiding Chat Button on page load
        embeddedservice_bootstrap.settings.hideChatButtonOnLoad = true;

        /* START:: Conversation Opened Listener */
        window.addEventListener("onEmbeddedMessagingConversationOpened", (event) => {
          hideChatContainer();
        });
        /* END:: Conversation Opened Listener */

        /* START:: Conversation Closed Listener */
        window.addEventListener("onEmbeddedMessagingWindowClosed", (event) => {
          showChatContainer();
        });
        /* END:: Conversation Closed Listener */

        /* START:: Button Created Listener */
        window.addEventListener("onEmbeddedMessagingButtonCreated", (event) => {
          showChatContainer();
        });
        /* END:: Button Created Listener */

        embeddedservice_bootstrap.init(
          '00DHo000002fRR9',
          'MIAW',
          'https://infallibletechie2-dev-ed.develop.my.site.com/ESWMIAW1754416406121',
          {
            scrt2URL: 'https://infallibletechie2-dev-ed.develop.my.salesforce-scrt.com'
          }
        );
      } catch (err) {
        console.error('Error loading Embedded Messaging: ', err);
      }
    }
  </script>

  <script 
    type="text/javascript" 
    src="https://infallibletechie2-dev-ed.develop.my.site.com/ESWMIAW1754416406121/assets/js/bootstrap.min.js" 
    onload="initEmbeddedMessaging()">
  </script>
</head>

<body>
  <div class="chat-container">
    <div>
      Welcome to our Chat!!!
      <br /><br /><br />
    </div>

    <div class="chat-input-area">
      <input 
        type="text" 
        id="chatInput" 
        class="chat-input" 
        placeholder="Type a message..." 
      />
      <button class="send-button" id="sendBtn">➤</button>
    </div>

    <div>
      <br/><br/>
      <button class="send-message-button" id="connectButton">
        Connect me with a sales rep
      </button>
    </div>
  </div>

  <script>
    function showChatContainer() {
      const chatContainer = document.querySelector('.chat-container');
      chatContainer.style.display = 'block';
    }

    function hideChatContainer() {
      const chatContainer = document.querySelector('.chat-container');
      chatContainer.style.display = 'none';
    }

    function launchChat() {
      embeddedservice_bootstrap.utilAPI.launchChat()
          .then(() => {
            console.log('Successfully launched Messaging');
          })
          .catch(() => {
            console.log('Some error occurred when launching Messaging');
          })
          .finally(() => {
            console.log('Successfully launched Messaging - Finally');
          });
    }

    function sendMessageToChat(message) {
      setTimeout(() => {
          embeddedservice_bootstrap.utilAPI.sendTextMessage(message)
            .then(() => {
              console.log("Message sent");
            })
            .catch(() => {
              console.log("Message not sent");
            })
            .finally(() => {
              console.log("Message sent - finally");
            });
        }, 3000);
    }

    const sendBtn = document.getElementById('sendBtn');
    const chatInput = document.getElementById('chatInput');

    sendBtn.addEventListener('click', () => {
      const message = chatInput.value.trim();
      if (message) {
        console.log(message);
        chatInput.value = '';
        hideChatContainer();

        launchChat();

        sendMessageToChat(message);
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

    // Get the button element using its ID
    const button = document.getElementById('connectButton');
    
    // Add an event listener that runs a function when the button is clicked
    button.addEventListener('click', function() {
      // Get the text content of the button
      const buttonText = button.textContent.trim();
      
      // Display the text in the browser's console
      console.log(buttonText);
      launchChat();
      sendMessageToChat(buttonText);
    });
  </script>
</body>
</html>
