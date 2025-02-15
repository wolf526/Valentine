<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chúc Mừng Valentine</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #FF69B4 !important; /* Màu hồng */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        .container {
            text-align: center;
            padding: 50px;
            border-radius: 10px;
            background-color: #ffffff;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }

        .heart-btn {
            font-size: 5rem;
            cursor: pointer;
            color: #ff4081;
            background: none;
            border: none;
            transition: transform 0.3s;
        }

        .heart-btn:hover {
            transform: scale(1.2);
        }

        .message {
            font-size: 1.5rem;
            color: #333;
            margin-top: 20px;
        }

        /* Pháo hoa */
        .fireworks {
            position: absolute;
            top: 0;
            left: 0;
            z-index: 9999;
            pointer-events: none;
            display: none;
            width: 100vw;
            height: 100vh;
        }

        .firework {
            position: absolute;
            width: 15px;
            height: 15px;
            border-radius: 50%;
            animation: explode 1s forwards;
        }

        @keyframes explode {
            0% {
                transform: scale(1);
                opacity: 1;
            }
            100% {
                transform: scale(6);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <button class="heart-btn" onclick="showFireworks()">❤️</button>
        <div class="message">Chúc Mừng Valentine, Bé Yêu! ❤️</div> <!-- Giữ lại dòng chữ -->
    </div>

    <div class="fireworks" id="fireworks"></div>

    <!-- Âm thanh khi bắn pháo hoa -->
    <audio id="fireworkSound" src="firework.mp3" preload="auto"></audio>

    <script>
        function getRandomColor() {
            const colors = ['#ff4081', '#ffeb3b', '#4caf50', '#2196f3', '#9c27b0', '#ff5722', '#00bcd4'];
            return colors[Math.floor(Math.random() * colors.length)];
        }

        function playFireworkSound() {
            const sound = document.getElementById('fireworkSound');
            sound.currentTime = 0;
            sound.play();
        }

        function showFireworks() {
            const fireworksContainer = document.getElementById('fireworks');
            fireworksContainer.style.display = 'block';

            let round = 0;
            const interval = setInterval(() => {
                playFireworkSound();

                for (let i = 0; i < 10; i++) {
                    const firework = document.createElement('div');
                    firework.classList.add('firework');
                    firework.style.backgroundColor = getRandomColor();

                    const randomX = Math.random() * 100;
                    const randomY = Math.random() * 100;

                    firework.style.left = `${randomX}vw`; 
                    firework.style.top = `${randomY}vh`;

                    setTimeout(() => {
                        firework.remove();
                    }, 3000);

                    fireworksContainer.appendChild(firework);
                }

                round++;
                if (round === 10) {
                    clearInterval(interval);
                    setTimeout(() => {
                        fireworksContainer.style.display = 'none';
                    }, 7000);
                }
            }, 3000);
        }
    </script>
</body>
</html>
