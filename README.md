<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clicker Game</title>
</head>
<link rel="stylesheet" href="css/style.css">
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.game-container {
    text-align: center;
    background-color: #fff;
    border-radius: 8px;
    padding: 30px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

button {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 15px 32px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 10px;
}

button:hover {
    background-color: #45a049;
}
</link>
<body>
    <div class="game-container">
        <h1>Clicker Game</h1>
        <p id="score">Score: 0</p>
        <!-- Existing HTML for "Click me!" button -->
<button id="clickButton">Click me!</button>

<!-- Upgrade buttons -->
<p>Upgrade: <button id="upgradeButton">Double Score (Cost: 10)</button></p>
<p>Additional Upgrades:</p>
<button id="multiplierUpgrade">Increase Multiplier (Cost: 20)</button>
<button id="clickUpgrade">Increase Points per Click (Cost: 30)</button>
<button id="resetButton">Reset Game</button>  <!-- Button to trigger reset -->
<div id="achievementsDisplay"></div>

    </div>
    <script src="js/script.js">
let score = 0;  // Initial score
let scoreMultiplier = 1;  // Initial score multiplier
let clickPoints = 1;  // Points added per click
let upgradeCost = 10;  // Initial cost of the double score upgrade
let multiplierUpgradeCost = 20;  // Cost for the multiplier upgrade
let clickUpgradeCost = 30;  // Cost for the points per click upgrade

// Achievement tracking
let achievements = [];
let clickCount = 0;
let multiplierUpgradeCount = 0;
let clickUpgradeCount = 0;

const scoreDisplay = document.getElementById("score");
const clickButton = document.getElementById("clickButton");
const upgradeButton = document.getElementById("upgradeButton");
const multiplierUpgradeButton = document.getElementById("multiplierUpgrade");
const clickUpgradeButton = document.getElementById("clickUpgrade");

const achievementsDisplay = document.getElementById("achievementsDisplay"); // Display achievements
const resetButton = document.getElementById("resetButton");  // Get reset button

// Event listener for the "Click me!" button
clickButton.addEventListener("click", () => {
    score += clickPoints * scoreMultiplier;
    clickCount++;
    checkAchievements();
    updateScore();
});

// Event listener for the "Double Score" upgrade button
upgradeButton.addEventListener("click", () => {
    if (score >= upgradeCost) {
        score -= upgradeCost;
        scoreMultiplier *= 2;
        upgradeCost *= 2;
        updateScore();
        upgradeButton.innerHTML = `Double Score (Cost: ${upgradeCost})`;
        multiplierUpgradeCount++;
        checkAchievements();
    } else {
        alert("Not enough points to upgrade!");
    }
});

// Event listener for the "Increase Multiplier" upgrade
multiplierUpgradeButton.addEventListener("click", () => {
    if (score >= multiplierUpgradeCost) {
        score -= multiplierUpgradeCost;
        scoreMultiplier *= 1.5;
        multiplierUpgradeCost *= 2;
        updateScore();
        multiplierUpgradeButton.innerHTML = `Increase Multiplier (Cost: ${multiplierUpgradeCost})`;
        multiplierUpgradeCount++;
        checkAchievements();
    } else {
        alert("Not enough points for this upgrade!");
    }
});

// Event listener for the "Increase Points per Click" upgrade
clickUpgradeButton.addEventListener("click", () => {
    if (score >= clickUpgradeCost) {
        score -= clickUpgradeCost;
        clickPoints += 1;
        clickUpgradeCost *= 2;
        updateScore();
        clickUpgradeButton.innerHTML = `Increase Points per Click (Cost: ${clickUpgradeCost})`;
        clickUpgradeCount++;
        checkAchievements();
    } else {
        alert("Not enough points for this upgrade!");
    }
});

// Reset function
resetButton.addEventListener("click", () => {
    const confirmReset = confirm("Are you sure you want to reset the game?");
    if (confirmReset) {
        resetGame();
    }
});

// Function to reset the game
function resetGame() {
    // Reset only the score, achievements, and counters.
    score = 0;
    clickCount = 0;
    achievements = [];
    updateScore();
    achievementsDisplay.innerHTML = "<strong>Achievements:</strong><br>";

    // Keep upgrades intact:
    // Retain points per click and score multiplier upgrades, but reset their costs
    clickPoints = 1;
    scoreMultiplier = 1;
    upgradeCost = 10;
    multiplierUpgradeCost = 20;
    clickUpgradeCost = 30;

    // Reset upgrade counters
    multiplierUpgradeCount = 0;
    clickUpgradeCount = 0;

    alert("Game has been reset! Some progress has been retained.");
}

// Function to update the score display
function updateScore() {
    scoreDisplay.textContent = `Score: ${score}`;
}

// Function to check and unlock achievements
function checkAchievements() {
    // Score-based achievements
    if (score >= 1e3 && !achievements.includes('Score 1e3')) {
        achievements.push('Score 1e3');
        displayAchievements();
    }
    if (score >= 1e6 && !achievements.includes('Score 1e6')) {
        achievements.push('Score 1e6');
        displayAchievements();
    }
    if (score >= 1e9 && !achievements.includes('Score 1e9')) {
        achievements.push('Score 1e9');
        displayAchievements();
    }
    if (clickCount >= 100 && !achievements.includes('Click 100 times')) {
        achievements.push('Click 100 times');
        displayAchievements();
    }
}

// Function to display achievements
function displayAchievements() {
    achievementsDisplay.innerHTML = "<strong>Achievements:</strong><br>" + achievements.join("<br>");
}
    </script>
</body>
</html>
