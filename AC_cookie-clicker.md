---
layout: default
title: Cookie Clicker
units: "1,2,3,4,5,6"
course: csa
---

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
    table {
      margin-top: 20px;
      margin-left: auto;
      margin-right: auto;
    }
    table, th, td {
      border: 1px solid black;
      border-collapse: collapse;
    }
    th, td {
      padding: 10px;
    }
  </style>
</head>
<body>

  <h1>Cookie Clicker</h1>
  <p id="counter">Cookies: 0</p>
  <img id="cookie" src="cookie.png" alt="Cookie" onclick="clickCookie()">

  <p>Upgrades:</p>
  <table id="upgradeTable">
    <tr>
      <th>Upgrade</th>
      <th>Level</th>
      <th>Cost</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>Auto-Clicker</td>
      <td id="autoClickerLevel">0</td>
      <td>25 cookies</td>
      <td><button onclick="buyAutoClicker()">Buy</button></td>
    </tr>
    <tr>
      <td>+1 Cookie per Click</td>
      <td id="clickUpgradeLevel">0</td>
      <td>50 cookies</td>
      <td><button onclick="buyClickUpgrade()">Buy</button></td>
    </tr>
  </table>

  <script>
    let cookies = 0;
    let autoClickerLevel = 0;
    let clickUpgradeLevel = 0;

    function clickCookie() {
      cookies += 1 + clickUpgradeLevel; // +1 Cookie per Click upgrade
      updateCounter();
    }

    function updateCounter() {
      document.getElementById("counter").innerText = "Cookies: " + cookies;
    }

    // Auto-clicker upgrade
    function buyAutoClicker() {
      const autoClickerCost = 25;
      if (cookies >= autoClickerCost) {
        cookies -= autoClickerCost;
        autoClickerLevel++;
        updateCounter();

        // Perform the auto-click every second
        setInterval(function () {
          clickCookie();
        }, 1000);
        
        // Update Auto-Clicker level in the table
        document.getElementById("autoClickerLevel").innerText = autoClickerLevel;

        // Sort the table
        sortTable();
      } else {
        alert("Not enough cookies to buy an auto-clicker!");
      }
    }

    // +1 Cookie per Click upgrade
    function buyClickUpgrade() {
      const clickUpgradeCost = 50;
      if (cookies >= clickUpgradeCost) {
        cookies -= clickUpgradeCost;
        clickUpgradeLevel++;
        updateCounter();

        // Update +1 Cookie per Click level in the table
        document.getElementById("clickUpgradeLevel").innerText = clickUpgradeLevel;

        // Sort the table
        sortTable();
      } else {
        alert("Not enough cookies to buy the +1 Cookie per Click upgrade!");
      }
    }

    // Sort the table based on the Level column
    function sortTable() {
      let table = document.getElementById("upgradeTable");
      let rows, switching, i, x, y, shouldSwitch;
      switching = true;
      
      while (switching) {
        switching = false;
        rows = table.rows;

        for (i = 1; i < rows.length - 1; i++) {
          shouldSwitch = false;
          x = parseInt(rows[i].getElementsByTagName("td")[1].innerText);
          y = parseInt(rows[i + 1].getElementsByTagName("td")[1].innerText);

          if (x < y) {
            shouldSwitch = true;
            break;
          }
        }

        if (shouldSwitch) {
          rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
          switching = true;
        }
      }
    }
  </script>

</body>
</html>