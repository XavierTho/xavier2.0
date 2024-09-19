---
toc: false
comments: false
layout: post
title: "Cookie Clicker"
type: ccc
courses: { capsule: {week: 0} }
---

<head>
    <title>Cookie Clicker Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #e0e0e0;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }
        #game-container {
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            padding: 20px;
            width: 350px;
            text-align: center;
        }
        #cookie {
            width: 150px;
            height: 150px;
            background-image: url('https://img.icons8.com/emoji/200/000000/cookie-emoji.png');
            background-size: cover;
            border: none;
            cursor: pointer;
            transition: transform 0.1s ease;
        }
        #cookie:active {
            transform: scale(0.9);
        }
        #score {
            font-size: 28px;
            margin: 20px;
            color: #555;
        }
        #upgrades {
            margin: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .upgrade-button {
            margin: 5px;
            padding: 10px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 80%;
        }
        #reset {
            margin-top: 20px;
            padding: 10px;
            font-size: 16px;
            background-color: #f44336;
            color: white;
            border: none;
            cursor: pointer;
            width: 80%;
            border-radius: 5px;
        }
        .floating-number {
            position: absolute;
            font-size: 24px;
            color: gold;
            animation: floatUp 1s ease-out forwards;
        }
        @keyframes floatUp {
            0% {
                opacity: 1;
                transform: translateY(0);
            }
            100% {
                opacity: 0;
                transform: translateY(-50px);
            }
        }
    </style>
</head>
<body>
    <div id="game-container">
        <h1>Cookie Clicker</h1>
        <button id="cookie" onclick="clickCookie()"></button>
        <div id="score">Cookies: 0</div>
        <div id="upgrades">
            <button class="upgrade-button" id="cursor" onclick="buyCursor()">Buy Cursor (Cost: 10 cookies)</button>
            <button class="upgrade-button" id="grandma" onclick="buyGrandma()">Buy Grandma (Cost: 100 cookies)</button>
            <button class="upgrade-button" id="farm" onclick="buyFarm()">Buy Farm (Cost: 500 cookies)</button>
            <button class="upgrade-button" id="factory" onclick="buyFactory()">Buy Factory (Cost: 2000 cookies)</button>
        </div>
        <button id="reset" onclick="resetGame()">Reset Game</button>
    </div>

<script>
    var cookies = parseInt(localStorage.getItem('cookies')) || 0;
    var cursors = parseInt(localStorage.getItem('cursors')) || 0;
    var grandmas = parseInt(localStorage.getItem('grandmas')) || 0;
    var farms = parseInt(localStorage.getItem('farms')) || 0;
    var factories = parseInt(localStorage.getItem('factories')) || 0;

    var cursorCost = parseInt(localStorage.getItem('cursorCost')) || 10;
    var grandmaCost = parseInt(localStorage.getItem('grandmaCost')) || 100;
    var farmCost = parseInt(localStorage.getItem('farmCost')) || 500;
    var factoryCost = parseInt(localStorage.getItem('factoryCost')) || 2000;

    function clickCookie() {
        cookies++;
        showFloatingNumber();
        animateCookie();
        updateScore();
    }

    function animateCookie() {
        var cookie = document.getElementById('cookie');
        cookie.style.transform = 'scale(0.9)';
        setTimeout(function() {
            cookie.style.transform = 'scale(1)';
        }, 100);
    }

    function showFloatingNumber() {
        var floatNum = document.createElement('div');
        floatNum.innerHTML = '+1';
        floatNum.className = 'floating-number';
        floatNum.style.left = (window.innerWidth / 2) + 'px'; 
        floatNum.style.top = (window.innerHeight / 2) + 'px';
        document.body.appendChild(floatNum);
        setTimeout(function() {
            floatNum.remove();
        }, 1000);
    }

    function updateScore() {
        document.getElementById('score').innerHTML = 'Cookies: ' + cookies;
        saveProgress();
    }

    function buyCursor() {
        if (cookies >= cursorCost) {
            cookies -= cursorCost;
            cursors++;
            cursorCost = Math.floor(cursorCost * 1.15);
            document.getElementById('cursor').innerHTML = 'Buy Cursor (Cost: ' + cursorCost + ' cookies)';
            setInterval(function() {
                cookies += cursors;
                updateScore();
            }, 1000);
        }
    }

    function buyGrandma() {
        if (cookies >= grandmaCost) {
            cookies -= grandmaCost;
            grandmas++;
            grandmaCost = Math.floor(grandmaCost * 1.15);
            document.getElementById('grandma').innerHTML = 'Buy Grandma (Cost: ' + grandmaCost + ' cookies)';
            setInterval(function() {
                cookies += grandmas * 5;
                updateScore();
            }, 1000);
        }
    }

    function buyFarm() {
        if (cookies >= farmCost) {
            cookies -= farmCost;
            farms++;
            farmCost = Math.floor(farmCost * 1.15);
            document.getElementById('farm').innerHTML = 'Buy Farm (Cost: ' + farmCost + ' cookies)';
            setInterval(function() {
                cookies += farms * 20;
                updateScore();
            }, 1000);
        }
    }

    function buyFactory() {
        if (cookies >= factoryCost) {
            cookies -= factoryCost;
            factories++;
            factoryCost = Math.floor(factoryCost * 1.15);
            document.getElementById('factory').innerHTML = 'Buy Factory (Cost: ' + factoryCost + ' cookies)';
            setInterval(function() {
                cookies += factories * 50;
                updateScore();
            }, 1000);
        }
    }

    function resetGame() {
        cookies = 0;
        cursors = 0;
        grandmas = 0;
        farms = 0;
        factories = 0;

        cursorCost = 10;
        grandmaCost = 100;
        farmCost = 500;
        factoryCost = 2000;

        document.getElementById('cursor').innerHTML = 'Buy Cursor (Cost: ' + cursorCost + ' cookies)';
        document.getElementById('grandma').innerHTML = 'Buy Grandma (Cost: ' + grandmaCost + ' cookies)';
        document.getElementById('farm').innerHTML = 'Buy Farm (Cost: ' + farmCost + ' cookies)';
        document.getElementById('factory').innerHTML = 'Buy Factory (Cost: ' + factoryCost + ' cookies)';
        
        updateScore();
        saveProgress();
    }

    function saveProgress() {
        localStorage.setItem('cookies', cookies);
        localStorage.setItem('cursors', cursors);
        localStorage.setItem('grandmas', grandmas);
        localStorage.setItem('farms', farms);
        localStorage.setItem('factories', factories);
        localStorage.setItem('cursorCost', cursorCost);
        localStorage.setItem('grandmaCost', grandmaCost);
        localStorage.setItem('farmCost', farmCost);
        localStorage.setItem('factoryCost', factoryCost);
    }

    function loadProgress() {
        document.getElementById('cursor').innerHTML = 'Buy Cursor (Cost: ' + cursorCost + ' cookies)';
        document.getElementById('grandma').innerHTML = 'Buy Grandma (Cost: ' + grandmaCost + ' cookies)';
        document.getElementById('farm').innerHTML = 'Buy Farm (Cost: ' + farmCost + ' cookies)';
        document.getElementById('factory').innerHTML = 'Buy Factory (Cost: ' + factoryCost + ' cookies)';
        updateScore();
    }

    // Load saved progress and start the game
    loadProgress();
</script>
</body>
