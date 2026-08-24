---
layout: index
title: "Rock Paper Scissors: Expert Mode"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Game History"
description: "Roshambo on Expert Mode"
user-story: "As a player, I want to play Roshambo against the computer and view my game history so that I can see the results of my previous games."
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
