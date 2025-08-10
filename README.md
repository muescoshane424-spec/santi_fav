<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Catch My Heart ❤️</title>
<style>
    body {
        margin: 0;
        padding: 0;
        background: linear-gradient(135deg, #ff4b5c, #ffb84d);
        font-family: Arial, sans-serif;
        overflow: hidden;
        color: white;
    }
    #score {
        position: fixed;
        top: 10px;
        left: 50%;
        transform: translateX(-50%);
        font-size: 1.5rem;
        font-weight: bold;
        background: rgba(0,0,0,0.2);
        padding: 8px 16px;
        border-radius: 10px;
    }
    #basket {
        position: fixed;
        bottom: 20px;
        width: 80px;
        height: 40px;
        background: #fff;
        border-radius: 10px;
        border: 3px solid #f44336;
    }
    .heart {
        position: fixed;
        width: 30px;
        height: 30px;
        background: red;
        clip-path: polygon(50% 0%, 61% 5%, 75% 19%, 85% 34%, 92% 50%, 100% 68%, 90% 85%, 75% 100%, 50% 90%, 25% 100%, 10% 85%, 0% 68%, 8% 50%, 15% 34%, 25% 19%, 39% 5%);
    }
    #message {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(255,255,255,0.9);
        color: #ff4b5c;
        padding: 20px;
        border-radius: 15px;
        text-align: center;
        font-size: 1.5rem;
        display: none;
    }
    #message button {
        margin-top: 15px;
        padding: 10px 20px;
        background: #ffb84d;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        font-size: 1rem;
        color: white;
    }
</style>
</head>
<body>

<div id="score">Score: 0</div>
<div id="basket"></div>
<div id="message">
    <p>You won my heart! 💍<br>Will you be my husband?</p>
    <button onclick="alert('Yay! 💖')">Yes 💖</button>
</div>

<script>
    const basket = document.getElementById('basket');
    const scoreDisplay = document.getElementById('score');
    const message = document.getElementById('message');
    let basketX = window.innerWidth / 2 - 40;
    let score = 0;
    let gameRunning = true;

    // Position basket initially
    basket.style.left = basketX + 'px';

    // Keyboard controls
    document.addEventListener('keydown', e => {
        if (!gameRunning) return;
        if (e.key === 'ArrowLeft') basketX -= 20;
        if (e.key === 'ArrowRight') basketX += 20;
        basketX = Math.max(0, Math.min(window.innerWidth - 80, basketX));
        basket.style.left = basketX + 'px';
    });

    // Mobile touch controls
    document.addEventListener('touchmove', e => {
        if (!gameRunning) return;
        basketX = e.touches[0].clientX - 40;
        basketX = Math.max(0, Math.min(window.innerWidth - 80, basketX));
        basket.style.left = basketX + 'px';
    });

    // Create falling hearts
    function createHeart() {
        if (!gameRunning) return;
        const heart = document.createElement('div');
        heart.classList.add('heart');
        heart.style.left = Math.random() * (window.innerWidth - 30) + 'px';
        heart.style.top = '0px';
        document.body.appendChild(heart);

        let heartY = 0;
        const fall = setInterval(() => {
            if (!gameRunning) {
                heart.remove();
                clearInterval(fall);
                return;
            }
            heartY += 4;
            heart.style.top = heartY + 'px';

            // Collision check
            const basketRect = basket.getBoundingClientRect();
            const heartRect = heart.getBoundingClientRect();
            if (
                heartRect.bottom >= basketRect.top &&
                heartRect.left >= basketRect.left &&
                heartRect.right <= basketRect.right
            ) {
                score++;
                scoreDisplay.textContent = 'Score: ' + score;
                heart.remove();
                clearInterval(fall);

                if (score >= 15) {
                    endGame();
                }
            }

            // Remove if falls off screen
            if (heartY > window.innerHeight) {
                heart.remove();
                clearInterval(fall);
            }
        }, 20);

        // Spawn next heart
        setTimeout(createHeart, 800 + Math.random() * 600);
    }

    function endGame() {
        gameRunning = false;
        message.style.display = 'block';
    }

    createHeart();
</script>

</body>
</html>
