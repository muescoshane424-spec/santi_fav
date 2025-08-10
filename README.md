<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Will You Be My Boyfriend?</title>
<style>
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        background: linear-gradient(135deg, #ff4b5c, #ffb84d);
        color: white;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin: 0;
        overflow: hidden;
    }
    h1 {
        font-size: 2.5rem;
        margin-bottom: 30px;
        animation: popIn 1s ease;
    }
    button {
        padding: 15px 30px;
        font-size: 1.2rem;
        margin: 10px;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        transition: 0.3s;
    }
    #yes {
        background-color: #4CAF50;
        color: white;
    }
    #no {
        background-color: #f44336;
        color: white;
        position: absolute;
    }
    @keyframes popIn {
        0% { transform: scale(0.5); opacity: 0; }
        100% { transform: scale(1); opacity: 1; }
    }
    .heart {
        position: fixed;
        bottom: -20px;
        color: #ff3366;
        font-size: 20px;
        animation: floatUp 4s linear infinite;
    }
    @keyframes floatUp {
        0% { transform: translateY(0) scale(1); opacity: 1; }
        100% { transform: translateY(-100vh) scale(1.5); opacity: 0; }
    }
</style>
</head>
<body>

<h1 id="question">Will you be my boyfriend? ❤️</h1>
<div>
    <button id="yes" onclick="sayYes()">Yes</button>
    <button id="no" onmouseover="moveButton()" onclick="angryReaction()">No</button>
</div>

<script>
let angryCount = 0;
const angryMessages = [
    "😡 Hey! That’s not nice!",
    "😤 You better think again!",
    "💢 Now you’re testing me!",
    "😠 Grrr!",
    "😾 Okay, now I’m really mad!",
    "😡 FINAL WARNING! Click YES!"
];

function sayYes() {
    document.body.innerHTML = `
        <h1>Yay! ❤️ You're mine now 😘</h1>
        <img src="https://media.tenor.com/2roX3uxz_68AAAAM/cute-love.gif" width="250">
    `;
    startHearts();
}

function moveButton() {
    const btn = document.getElementById("no");
    const x = Math.random() * (window.innerWidth - btn.clientWidth);
    const y = Math.random() * (window.innerHeight - btn.clientHeight);
    btn.style.left = x + "px";
    btn.style.top = y + "px";
}

function angryReaction() {
    angryCount++;
    const question = document.getElementById("question");
    if (angryCount < angryMessages.length) {
        question.innerText = angryMessages[angryCount - 1];
    } else {
        question.innerText = "😡 THAT’S IT, I’M TAKING OVER!";
    }
}

// Floating hearts generator
function startHearts() {
    setInterval(() => {
        const heart = document.createElement("div");
        heart.className = "heart";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.fontSize = Math.random() * 20 + 15 + "px";
        heart.innerText = "❤️";
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 4000);
    }, 300);
}
</script>

</body>
</html>
