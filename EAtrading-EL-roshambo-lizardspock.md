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
    // Randomize computer choice from all 5 options
    const choices = ['rock', 'paper', 'scissors', 'lizard', 'spock'];
    const serverGesture = choices[Math.floor(Math.random() * choices.length)];
    
    // Rock Paper Scissors Lizard Spock rules
    const wins = {
        rock: ['scissors', 'lizard'],
        paper: ['rock', 'spock'],
        scissors: ['paper', 'lizard'],
        lizard: ['paper', 'spock'],
        spock: ['rock', 'scissors']
    };
    
    let result;
    if (clientGesture === serverGesture) {
        result = "tie";
    } else if (wins[clientGesture].includes(serverGesture)) {
        result = "win";
    } else {
        result = "lose";
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
