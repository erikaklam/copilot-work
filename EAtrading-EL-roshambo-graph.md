---
layout: minimal-bootstrap
title: "Rock Paper Scissors: Historical Results Graph"
heading: "Rock Paper Roshambo in JavaScript"
subheading: "Data Analysis"
description: "Roshambo with Historical Results Graph"
user-story: "As a data scientist, I want to add a historical result graph so that I can analyze results"
---

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

Which one will it be?

<a href="#" onclick="playRoshambo('rock')">rock</a>
<a href="#" onclick="playRoshambo('paper')">paper</a>
<a href="#" onclick="playRoshambo('scissors')">scissors</a>

<br/>

<div id="results"></div>
<canvas id="resultsChart" width="400" height="200"></canvas>
<br/>
<div id="history"></div>


<script>
games = JSON.parse(localStorage.getItem('games')) || [];
let resultsChart = null;

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
    updateChart();
}

deleteGame = function(time) {
    games = games.filter(game => game.time != time);
    localStorage.setItem('games', JSON.stringify(games));
    showHistory();
    updateChart();
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

updateChart = function() {
    // Calculate wins, losses, and ties
    const wins = games.filter(g => g.result === 'win').length;
    const losses = games.filter(g => g.result === 'lose').length;
    const ties = games.filter(g => g.result === 'tie').length;
    
    const ctx = document.getElementById('resultsChart').getContext('2d');
    
    if (resultsChart) {
        resultsChart.destroy();
    }
    
    resultsChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['Wins', 'Losses', 'Ties'],
            datasets: [{
                label: 'Game Results',
                data: [wins, losses, ties],
                backgroundColor: [
                    'rgba(75, 192, 192, 0.6)',
                    'rgba(255, 99, 132, 0.6)',
                    'rgba(255, 206, 86, 0.6)'
                ],
                borderColor: [
                    'rgba(75, 192, 192, 1)',
                    'rgba(255, 99, 132, 1)',
                    'rgba(255, 206, 86, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            scales: {
                y: {
                    beginAtZero: true,
                    ticks: {
                        stepSize: 1
                    }
                }
            }
        }
    });
}

// Initialize chart on page load
window.addEventListener('load', function() {
    updateChart();
});

</script>
