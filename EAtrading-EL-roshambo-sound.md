---
layout: minimal-bootstrap
title: "Rock Paper Scissors: Sound Effects"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Enhanced Gameplay"
description: "Roshambo with Sound Effects"
user-story: "As a player I Want to add sound effects, so that I can have better gameplay"
---

Which one will it be?

<a href="#" onclick="playRoshambo('rock')">rock</a>
<a href="#" onclick="playRoshambo('paper')">paper</a>
<a href="#" onclick="playRoshambo('scissors')">scissors</a>

<br/>

<div id="history"></div>
<div id="results"></div>


<script>
games = JSON.parse(localStorage.getItem('games')) || [];
playRoshambo = function(clientGesture){
    if (clientGesture=='rock') {
        result = "lose";
    }
    if (clientGesture=='paper') {
        result = "win";
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
