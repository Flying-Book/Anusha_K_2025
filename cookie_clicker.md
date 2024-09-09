---
layout: post
title: Cookie Clicker
description: Cookie Clicker Game
permalink: /cookie
comments: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker</title>
    <style>
        body {
            background-image: url('https://cdn.vectorstock.com/i/500p/57/28/bakery-seamless-background-vector-27135728.jpg');
            background-size: cover;
            background-position: center;
            margin: 0;
            font-family: 'Arial', sans-serif;
            height: 100vh;
            overflow: hidden; /* Prevent scrolling */
        }

        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.5);
            pointer-events: none;
            opacity: 0;
            transition: opacity 1s ease, background-color 1s ease;
        }

        .show-overlay {
            opacity: 1;
        }

        .container {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            background-color: rgba(255, 255, 255, 0.8);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            z-index: 1;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            color: #f57c00;
        }

        #cookie-container {
            margin: 20px 0;
        }

        #cookie {
            width: 150px;
            cursor: pointer;
            transition: transform 0.1s;
        }

        #cookie:active {
            transform: scale(0.95);
        }

        #counter {
            font-size: 1.5rem;
            color: #f57c00;
            margin: 20px 0;
        }

        .upgrade-btn {
            background-color: #f57c00;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 1rem;
            cursor: pointer;
            border-radius: 5px;
            margin: 5px;
            transition: background-color 0.3s;
        }

        .upgrade-btn:hover {
            background-color: #d65a00;
        }

        .upgrade-btn:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }

        #congratulations {
            font-size: 1.5rem;
            color: #ff5722;
            display: none;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="overlay" id="overlay"></div>
    <div class="container">
        <h1>Cookie Clicker</h1>
        <div id="cookie-container">
            <img class="img-responsive" id="cookie" src="https://upload.wikimedia.org/wikipedia/commons/7/70/Cookie.png" alt="Cookie">
        </div>
        <p id="counter">Cookies: 0</p>
        <button id="upgrade-btn-1" class="upgrade-btn">Upgrade 1 (Cost: 50)</button>
        <button id="upgrade-btn-2" class="upgrade-btn">Upgrade 2 (Cost: 100)</button>
        <button id="upgrade-btn-3" class="upgrade-btn">Upgrade 3 (Cost: 200)</button>
        <p id="congratulations">Congratulations! You've reached a milestone!</p>
    </div>
    <script>
        let cookies = 0;
        let cookiesPerClick = 1;

        const cookie = document.getElementById('cookie');
        const counter = document.getElementById('counter');
        const upgradeBtn1 = document.getElementById('upgrade-btn-1');
        const upgradeBtn2 = document.getElementById('upgrade-btn-2');
        const upgradeBtn3 = document.getElementById('upgrade-btn-3');
        const overlay = document.getElementById('overlay');
        const congratulations = document.getElementById('congratulations');

        cookie.addEventListener('click', () => {
            cookies += cookiesPerClick;
            counter.textContent = `Cookies: ${cookies}`;
            checkUpgrades();
            triggerEffect();
        });

        upgradeBtn1.addEventListener('click', () => {
            if (cookies >= 50) {
                cookies -= 50;
                cookiesPerClick++;
                counter.textContent = `Cookies: ${cookies}`;
                checkUpgrades();
            }
        });

        upgradeBtn2.addEventListener('click', () => {
            if (cookies >= 100) {
                cookies -= 100;
                cookiesPerClick += 2;
                counter.textContent = `Cookies: ${cookies}`;
                checkUpgrades();
            }
        });

        upgradeBtn3.addEventListener('click', () => {
            if (cookies >= 200) {
                cookies -= 200;
                cookiesPerClick += 5;
                counter.textContent = `Cookies: ${cookies}`;
                checkUpgrades();
            }
        });

        function checkUpgrades() {
            upgradeBtn1.disabled = cookies < 50;
            upgradeBtn2.disabled = cookies < 100;
            upgradeBtn3.disabled = cookies < 200;
        }

        function triggerEffect() {
            if (cookies >= 200) {
                overlay.style.backgroundColor = 'rgba(0, 0, 255, 0.5)';
                congratulations.style.display = 'block';
            } else if (cookies >= 100) {
                overlay.style.backgroundColor = 'rgba(0, 255, 0, 0.5)';
                congratulations.style.display = 'none';
            } else if (cookies >= 50) {
                overlay.style.backgroundColor = 'rgba(255, 0, 0, 0.5)';
                congratulations.style.display = 'none';
            } else {
                overlay.style.backgroundColor = 'rgba(255, 255, 255, 0.5)';
                congratulations.style.display = 'none';
            }

            overlay.classList.add('show-overlay');
            setTimeout(() => {
                overlay.classList.remove('show-overlay');
            }, 1000); // Effect lasts 1 second
        }
    </script>
</body>
</html>
