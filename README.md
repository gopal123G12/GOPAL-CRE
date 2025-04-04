# GOPAL-CRE
<br>IN MY RESPONSIBILITY
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #282c34;
        }
        canvas {
            background-color: black;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="400" height="400"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        const box = 20;
        let snake = [{ x: 10 * box, y: 10 * box }];
        let direction = "RIGHT";
        let food = {
            x: Math.floor(Math.random() * 20) * box,
            y: Math.floor(Math.random() * 20) * box,
        };

        document.addEventListener("keydown", changeDirection);
        function changeDirection(event) {
            const key = event.keyCode;
            if (key === 37 && direction !== "RIGHT") direction = "LEFT";
            else if (key === 38 && direction !== "DOWN") direction = "UP";
            else if (key === 39 && direction !== "LEFT") direction = "RIGHT";
            else if (key === 40 && direction !== "UP") direction = "DOWN";
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "red";
            ctx.fillRect(food.x, food.y, box, box);
            
            for (let i = 0; i < snake.length; i++) {
                ctx.fillStyle = i === 0 ? "lime" : "green";
                ctx.fillRect(snake[i].x, snake[i].y, box, box);
            }

            let snakeX = snake[0].x;
            let snakeY = snake[0].y;

            if (direction === "LEFT") snakeX -= box;
            if (direction === "RIGHT") snakeX += box;
            if (direction === "UP") snakeY -= box;
            if (direction === "DOWN") snakeY += box;

            if (snakeX === food.x && snakeY === food.y) {
                food = {
                    x: Math.floor(Math.random() * 20) * box,
                    y: Math.floor(Math.random() * 20) * box,
                };
            } else {
                snake.pop();
            }

            let newHead = { x: snakeX, y: snakeY };
            if (
                snakeX < 0 || snakeX >= canvas.width ||
                snakeY < 0 || snakeY >= canvas.height ||
                snake.some(segment => segment.x === newHead.x && segment.y === newHead.y)
            ) {
                clearInterval(game);
                alert("Game Over!");
                return;
            }
            snake.unshift(newHead);
        }

        let game = setInterval(draw, 100);
    </script>
</body>
</html>
