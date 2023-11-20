---
layout: default
title: DuClick
units: "1,2,3,4,5,6"
course: csa
---

<style>
    body {
        font-family: 'Kavoon', cursive;
        background: #3999e3; /* Fallback color in case the gradient doesn't load */
        background: repeating-linear-gradient(to right, #3578ab, #3578ab 1%, #3999e3 1%, #3999e3 2%);
        margin: 0; /* Remove default margin */
        padding: 0; /* Remove default padding */
    }

    @keyframes floatAnimation {
        0%, 100% {
            transform: translateY(10px);
        }
        50% {
            transform: translateY(-10px);
        }
    }

    #cookie {
        width: 75%;
        margin-left: 5%;
        margin-top: 5%;
        margin-bottom: 5%;
        animation: floatAnimation 2s ease-in-out infinite;
        border-radius: 100px; /* Add rounded edges to the image */
        overflow: hidden; /* Ensure the rounded corners are applied */
    }

    .upgrade {
        color: #121212;
        transition: color 0.3s ease;
        cursor: pointer;
    }

    .upgrade:hover {
        color: yellow;
    }

    .game-container table, .game-container tr {
        margin-top: 5%;
        border: 2px solid rgba(18, 18, 18, 0); /* Transparent border color */
        border-radius: 50px; /* Add rounded edges to the table */
        background-color: rgba(18, 18, 18, 0); /* Transparent background color */
        overflow: hidden; /* Ensure the rounded corners are applied */
    }

    button {
        background-color: #4CAF50; /* Green background color */
        border: none;
        color: white;
        padding: 10px 20px; /* Adjust padding as needed */
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        border-radius: 10px; /* Add rounded edges to the button */
        cursor: pointer;
        transition: background-color 0.3s ease; /* Add a smooth transition effect */
    }

    button:hover {
        background-color: #45a049; /* Darker green color on hover */
    }

    .game-container tr:hover {
        background-color: rgba(255, 255, 0, 0.2); /* Transparent yellow background color on hover */
    }
</style>

<link href="https://fonts.googleapis.com/css2?family=Kavoon&display=swap" rel="stylesheet">

<div class="game-container">
    <table class="mostly-centered-table">
        <tr>
            <td>
                <button><img id="cookie" src="images/cookie.jpg"></button>
            </td>
            <td>
                <table>
                    <thead>
                        <tr>
                            <th>Upgrade</th>
                            <th>Description</th>
                            <th>Level</th>
                            <th>Cost</th>
                            <th>Buy</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="upgrade">
                            <td>King</td>
                            <td>Plus Cookies</td>
                            <td>0</td>
                            <td>$20</td>
                            <td><button>Buy</button></td>
                        </tr>
                        <tr class="upgrade">
                            <td>Upgrade 2</td>
                            <td>Auto Cookies</td>
                            <td>2</td>
                            <td>$20</td>
                            <td><button>Buy</button></td>
                        </tr>
                    </tbody>
                </table>
            </td>
        </tr>
    </table>
</div>

<script>
    document.addEventListener('DOMContentLoaded', function() {
        
        var clickableElements = document.querySelectorAll('.upgrade');

        clickableElements.forEach(function(element) {
            element.addEventListener('click', upgrade);
        });

        function upgrade() {
            // write stuff here boyos
        }
    });
</script>