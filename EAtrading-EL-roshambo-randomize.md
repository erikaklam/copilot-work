---
layout: index
title: "Rock Paper Scissors: Randomize Computer Choice"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Competitive Play"
description: "Roshambo with Randomized Computer Moves"
user-story: "As a player I want to randomize computer choice, sothat I can play competitively"
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
    // Randomize computer choice
    const choices = ['rock', 'paper', 'scissors'];
    const serverGesture = choices[Math.floor(Math.random() * choices.length)];
    
    // Determine winner
    let result;
    if (clientGesture === serverGesture) {
        result = "tie";
    } else if (
        (clientGesture === 'rock' && serverGesture === 'scissors') ||
        (clientGesture === 'paper' && serverGesture === 'rock') ||
        (clientGesture === 'scissors' && serverGesture === 'paper')
    ) {
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
