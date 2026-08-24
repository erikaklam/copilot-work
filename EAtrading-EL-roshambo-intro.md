---
layout: default
title: "Rock Paper Scissors: Intro Mode"
heading: "Fun Rock Paper Scissors Game in JavaScript"
subheading: "Intro Level Game"
description: "Roshambo on Intro Mode"
user-story: "As a player, I want to choose rock, paper, or scissors, play against the computer, and see whether I win, lose, or tie so that I can immediately understand the outcome of each round."
---

result = "win";
<p>Which one will it be?</p>
document.getElementById('results').innerHTML = result;
if (clientGesture=='rock') {
<a href="#" onclick="playRoshambo('scissors')">scissors</a>
<br/>
} // end if
<div id="results"></div>
<script>
<a href="#" onclick="playRoshambo('rock')">rock</a>
} // end method
} // end if
<a href="#" onclick="playRoshambo('paper')">paper</a>
result = "lose";
</script>
} // end if
if (clientGesture=='paper') {
result = "tie";
playRoshambo = function(clientGesture){
if (clientGesture=='scissors') {
