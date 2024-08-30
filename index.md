---
layout: base
title: Anusha Khobare's Home Page 
description: Home Page
hide: true
---
Hi, my name is Anusha Khobare and I am intrested in computer-aided art. 
<html lang="en">
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #f0f8ff;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
    <canvas id="bubbleCanvas"></canvas>
    <script>
        const canvas = document.getElementById('bubbleCanvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const bubbles = [];
        const numBubbles = 50;

        function createBubble(x, y) {
            return {
                x,
                y,
                radius: Math.random() * 20 + 10,
                alpha: 1,
                speedX: (Math.random() - 0.5) * 2,
                speedY: (Math.random() - 0.5) * 2
            };
        }

        function drawBubble(bubble) {
            ctx.beginPath();
            ctx.arc(bubble.x, bubble.y, bubble.radius, 0, Math.PI * 2, false);
            ctx.fillStyle = `rgba(173, 216, 230, ${bubble.alpha})`; // Light blue color
            ctx.fill();
            ctx.closePath();
        }

        function updateBubbles() {
            bubbles.forEach(bubble => {
                bubble.x += bubble.speedX;
                bubble.y += bubble.speedY;
                bubble.alpha -= 0.01;
                if (bubble.alpha <= 0) {
                    bubble.alpha = 0;
                }
            });
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            updateBubbles();
            bubbles.forEach(drawBubble);
            requestAnimationFrame(animate);
        }

        canvas.addEventListener('mousemove', (e) => {
            for (let i = 0; i < numBubbles; i++) {
                bubbles.push(createBubble(e.clientX, e.clientY));
            }
        });

        animate();
    </script>
</html>
