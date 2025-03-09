# famous-ai-gpt
Famous AI GPT：專為全球用戶打造的高效 AI 助理，支援多語言與即時互動。
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Famous AI GPT</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        #chatbox { width: 80%; height: 300px; border: 1px solid #ccc; overflow-y: scroll; margin: auto; padding: 10px; }
        input { width: 70%; padding: 10px; margin-top: 10px; }
        button { padding: 10px; }
    </style>
</head>
<body>
    <h1>歡迎使用 Famous AI GPT</h1>
    <div id="chatbox"></div>
    <input type="text" id="userInput" placeholder="輸入您的問題..." />
    <button onclick="sendMessage()">送出</button>

    <script>
        function sendMessage() {
            const userInput = document.getElementById('userInput').value;
            if (!userInput) return;

            const chatbox = document.getElementById('chatbox');
            chatbox.innerHTML += `<p><strong>你：</strong> ${userInput}</p>`;

            fetch('/ask', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ message: userInput })
            })
            .then(response => response.json())
            .then(data => {
                chatbox.innerHTML += `<p><strong>Famous AI GPT：</strong> ${data.reply}</p>`;
                document.getElementById('userInput').value = '';
                chatbox.scrollTop = chatbox.scrollHeight;
            });
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Famous AI GPT</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        #chatbox { width: 80%; height: 300px; border: 1px solid #ccc; overflow-y: scroll; margin: auto; padding: 10px; }
        input { width: 70%; padding: 10px; margin-top: 10px; }
        button { padding: 10px; }
    </style>
</head>
<body>
    <h1>歡迎使用 Famous AI GPT</h1>
    <div id="chatbox"></div>
    <input type="text" id="userInput" placeholder="輸入您的問題..." />
    <button onclick="sendMessage()">送出</button>

    <script>
        function sendMessage() {
            const userInput = document.getElementById('userInput').value;
            if (!userInput) return;

            const chatbox = document.getElementById('chatbox');
            chatbox.innerHTML += `<p><strong>你：</strong> ${userInput}</p>`;

            fetch('/ask', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ message: userInput })
            })
            .then(response => response.json())
            .then(data => {
                chatbox.innerHTML += `<p><strong>Famous AI GPT：</strong> ${data.reply}</p>`;
                document.getElementById('userInput').value = '';
                chatbox.scrollTop = chatbox.scrollHeight;
            });
        }
    </script>
</body>
</html>
const express = require('express');
const cors = require('cors');

const app = express();
app.use(express.json());
app.use(cors());

app.post('/ask', (req, res) => {
    const userMessage = req.body.message;
    const botReply = generateResponse(userMessage);
    res.json({ reply: botReply });
});

// 簡單的 AI 回應函數
function generateResponse(message) {
    if (message.includes('你好')) return '你好！有什麼問題可以幫助你？';
    if (message.includes('天氣')) return '今天是晴天，適合出門散步！';
    return '很抱歉，我還無法理解您的問題，但我會努力學習！';
}

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`伺服器運行於 http://localhost:${PORT}`));
