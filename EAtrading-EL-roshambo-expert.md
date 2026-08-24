---
layout: default
title: "Rock Paper Scissors: Expert Mode"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Game History"
description: "Roshambo on Expert Mode"
user-story: "As a player, I want to play Roshambo against the computer and view my game history so that I can see the results of my previous games."
---

}
if (clientGesture=='rock') {
showHistory();
game = {
if (clientGesture=='paper') {
localStorage.setItem('games', JSON.stringify(games));
historyText = "";
historyText += "<a href='#' onclick=\"deleteGame('" + game.time + "')\">delete</a>";
historyText += game.clientGesture + " | ";
games = JSON.parse(localStorage.getItem('games')) || [];
localStorage.setItem('games', JSON.stringify(games));
for (game of games) {
Which one will it be?
<script>
historyText += "</div>";
<a href="#" onclick="playRoshambo('paper')">paper</a>
showHistory();
document.getElementById('results').innerHTML = result;
clientGesture: clientGesture,
historyText += game.time + " | ";
historyText += game.result + " | ";
games.push(game);
<div id="history"></div>
result = "win";
result: result,
}
}
result = "tie";
if (clientGesture=='scissors') {
historyText += "<div>";
<a href="#" onclick="playRoshambo('scissors')">scissors</a>
historyText += game.serverGesture + " | ";
result = "lose";
time: new Date()
serverGesture: serverGesture,
playRoshambo = function(clientGesture){
}
document.getElementById('history').innerHTML = historyText;
</script>
};
serverGesture = 'scissors';
deleteGame = function(time) {
}
showHistory = function() {
showHistory();
saveGame(clientGesture, serverGesture, result);
}
}
<br/>
<div id="results"></div>
games = games.filter(game => game.time != time);
<a href="#" onclick="playRoshambo('rock')">rock</a>
saveGame = function(clientGesture, serverGesture, result) {
}
