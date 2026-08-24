---
layout: minimal-bootstrap
title: "Rock Paper Scissors: Icons"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Enhanced UI"
description: "Roshambo with Icons"
user-story: "Aa a UX designer, I want to add icons to the game so that the user can have better UI"
---

<style>
.game-icon {
    width: 100px;
    height: 100px;
    margin: 10px;
    cursor: pointer;
    transition: transform 0.2s;
    border: 2px solid transparent;
    border-radius: 10px;
}
.game-icon:hover {
    transform: scale(1.1);
    border-color: #007bff;
}
</style>

Which one will it be?

<img src="rock.png" alt="Rock" class="game-icon" onclick="playRoshambo('rock')">
<img src="paper.png" alt="Paper" class="game-icon" onclick="playRoshambo('paper')">
<img src="scissors.png" alt="Scissors" class="game-icon" onclick="playRoshambo('scissors')">

<br/>

<div id="history"></div>
<div id="results"></div>


<script>
games = JSON.parse(localStorage.getItem('games')) || [];
playRoshambo = function(clientGesture){
    if (clientGesture=='rock') {
        result = "win";
    }
    if (clientGesture=='paper') {
        result = "lose";
    }
    if (clientGesture=='scissors') {
        result = "tie";
    }

    serverGesture = 'scissors';
    showHistory();
    document.getElementById('results').innerHTML = result;
    saveGame(clientGesture, serverGesture, result);
}

deleteGame = function(time) {
    games = games.filter(game => game.time != time);
    localStorage.setItem('games', JSON.stringify(games));
    showHistory();
}

showHistory = function() {
    historyText = "";
    for (game of games) {
        historyText += game.clientGesture + " | ";
        historyText += game.serverGesture + " | ";
        historyText += game.result + " | ";
        historyText += game.time + " | ";
        historyText += "<div>";
        historyText += "<a href='#' onclick=\"deleteGame('" + game.time + "')\">delete</a>";
        historyText += "</div>";
    };
    document.getElementById('history').innerHTML = historyText;
}

saveGame = function(clientGesture, serverGesture, result) {
    game = {
        clientGesture: clientGesture,
        serverGesture: serverGesture,
        result: result,
        time: new Date()
    }
    games.push(game);
    showHistory();
    localStorage.setItem('games', JSON.stringify(games));
}

</script>
