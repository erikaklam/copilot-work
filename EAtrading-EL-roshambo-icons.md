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
