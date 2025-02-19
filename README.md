<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sigma Snake Game</title>
    <style>
        body {
            text-align: center;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }
        canvas {
            background-color: #000;
            display: block;
            margin: 20px auto;
        }
    </style>
</head>
<body>
    <h1>Sigma Snake Game</h1>
    <canvas id="gameCanvas" width="400" height="400"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        const grid = 20;
        let count = 0;

        let snake = {
            x: 160,
            y: 160,
            dx: grid,
            dy: 0,
            cells: [],
            maxCells: 4
        };
        let apple = {
            x: 320,
            y: 320
        };

        function getRandomInt(min, max) {
            return Math.floor(Math.random() * (max - min)) + min;
        }

        function loop() {
            requestAnimationFrame(loop);

            if (++count < 4) {
                return;
            }

            count = 0;
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            snake.x += snake.dx;
            snake.y += snake.dy;

            if (snake.x < 0) {
                snake.x = canvas.width - grid;
            } else if (snake.x >= canvas.width) {
                snake.x = 0;
            }

            if (snake.y < 0) {
                snake.y = canvas.height - grid;
            } else if (snake.y >= canvas.height) {
                snake.y = 0;
            }

            snake.cells.unshift({x: snake.x, y: snake.y});

            if (snake.cells.length > snake.maxCells) {
                snake.cells.pop();
            }

            ctx.fillStyle = "red";
            ctx.fillRect(apple.x, apple.y, grid - 1, grid - 1);

            ctx.fillStyle = "blue";
            snake.cells.forEach(function (cell, index) {
                ctx.fillRect(cell.x, cell.y, grid - 1, grid - 1);

                if (cell.x === apple.x && cell.y === apple.y) {
                    snake.maxCells++;
                    apple.x = getRandomInt(0, 25) * grid;
                    apple.y = getRandomInt(0, 25) * grid;
                }

                for (let i = index + 1; i < snake.cells.length; i++) {
                    if (cell.x === ▋
