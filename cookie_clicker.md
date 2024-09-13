---
layout: post
title: Cookie Clicker
description: Cookie Clicker Game
permalink: /cookie
menu: nav/sprint_1.html
comments: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
        }
        #cookie-container {
            margin: 20px auto;
            display: flex;
            justify-content: center;
        }
        #cookie {
            width: 200px;
            cursor: pointer;
        }
        p {
            font-size: 1.2em;
        }
        #shop {
            margin-top: 20px;
        }
        #shop p {
            font-size: 1.2em;
        }
        #shop button {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div id="cookie-container">
        <img id="cookie" src="https://upload.wikimedia.org/wikipedia/commons/7/70/Cookie.png" alt="Cookie">
    </div>
    <p>Cookies: <span id="cookie-count">0</span></p>
    <p>Workers: <span id="worker-count">0</span></p>
    <p>Cookies left: <span id="cookies-left">0</span></p>
    <div id="shop">
        <p>Cost of 1 Worker: 5 Cookies</p>
        <button id="buy-worker">Buy Worker</button>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const cookieImage = document.getElementById('cookie');
            const cookieCountDisplay = document.getElementById('cookie-count');
            const workerCountDisplay = document.getElementById('worker-count');
            const cookiesLeftDisplay = document.getElementById('cookies-left');
            const buyWorkerButton = document.getElementById('buy-worker');
            const workerCost = 5;

            let cookieCount = 0;
            let workers = 0;
            let cookiesLeft = 0;
            let baseScore = 1;

            cookieImage.addEventListener('click', () => {
                cookieCount += baseScore;
                cookieCountDisplay.textContent = cookieCount;
            });

            buyWorkerButton.addEventListener('click', () => {
                if (cookieCount >= workerCost) {
                    cookieCount -= workerCost;
                    workers += 1;
                    baseScore = Math.pow(2, workers); // Each worker doubles the score
                    cookieCountDisplay.textContent = cookieCount;
                    workerCountDisplay.textContent = workers;
                    cookiesLeftDisplay.textContent = cookieCount;
                } else {
                    alert('Not enough cookies!');
                }
            });
            
            // Initialize display
            cookiesLeftDisplay.textContent = cookieCount;
        });
    </script>
</body>
</html>