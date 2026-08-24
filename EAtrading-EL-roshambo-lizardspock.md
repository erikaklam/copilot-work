---
layout: minimal-bootstrap
title: "Rock Paper Scissors: Lizard Spock"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Strategic Gameplay"
description: "Roshambo with Lizard and Spock"
user-story: "AS a user, I want to add lizard and spock so that players can have a more strategic game"
---

Which one will it be?

<a href="#" onclick="playRoshambo('rock')">rock</a>
<a href="#" onclick="playRoshambo('paper')">paper</a>
<a href="#" onclick="playRoshambo('scissors')">scissors</a>
<a href="#" onclick="playRoshambo('lizard')">lizard</a>
<a href="#" onclick="playRoshambo('spock')">spock</a>

<br/>

<div id="history"></div>
<div id="results"></div>


<script>
games = JSON.parse(localStorage.getItem('games')) || [];
playRoshambo = function(clientGesture){
    // Server always picks scissors
    serverGesture = 'scissors';
    
    // Determine result when server picks scissors
    let result;
    if (clientGesture == 'rock') {
        result = "win";  // rock beats scissors
    } else if (clientGesture == 'paper') {
        result = "lose";  // paper loses to scissors
    } else if (clientGesture == 'scissors') {
        result = "tie";  // scissors ties scissors
    } else if (clientGesture == 'lizard') {
        result = "lose";  // lizard loses to scissors
    } else if (clientGesture == 'spock') {
        result = "win";  // spock beats scissors
    }

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
