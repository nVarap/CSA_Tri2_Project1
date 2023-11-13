---
layout: default
title: CSSE
units: "1,2,3,4,5,6"
course: csse
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cookie Clicker</title>
  <style>
    body {
      text-align: center;
    }
    #cookie {
      width: 200px;
      height: 200px;
      margin-top: 50px;
      cursor: pointer;
    }
    #counter {
      font-size: 24px;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <h1>Cookie Clicker</h1>
  <p id="counter">Cookies: 0</p>
  <img id="cookie" src="cookie.png" alt="Cookie" onclick="clickCookie()">

  <script>
    let cookies = 0;

    function clickCookie() {
      cookies++;
      updateCounter();
    }

    function updateCounter() {
      document.getElementById("counter").innerText = "Cookies: " + cookies;
    }

    // Auto-clicker upgrade
    function buyAutoClicker() {
      const autoClickerCost = 10;
      if (cookies >= autoClickerCost) {
        cookies -= autoClickerCost;
        updateCounter();

        // Perform the auto-click every second
        setInterval(function () {
          clickCookie();
        }, 1000);
      } else {
        alert("Not enough cookies to buy an auto-clicker!");
      }
    }
  </script>

  <p>Buy an Auto-Clicker for 10 cookies:</p>
  <button onclick="buyAutoClicker()">Buy Auto-Clicker</button>

</body>
</html>