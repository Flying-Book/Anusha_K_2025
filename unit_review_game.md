---
layout: post
title: Unit Review Game
description: Unit Review Game
permalink: /unit_review_game
menu: nav/sprint_2.html
comments: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text-Based Adventure Game</title>
    <style>
        /* Basic styles for the game container */
        body {
            font-family: Arial, sans-serif; /* Sets font for the entire page */
            background-color: #f4f4f4; /* Light gray background */
            color: #333; /* Dark gray text color */
            margin: 0; /* Removes default margin */
            padding: 20px; /* Adds padding around the body */
        }

        .game-container {
            max-width: 600px; /* Maximum width of the game container */
            margin: auto; /* Centers the container */
            background: #fff; /* White background for the game area */
            padding: 20px; /* Padding inside the game area */
            border-radius: 5px; /* Rounded corners */
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /* Subtle shadow effect */
        }

        h1 {
            text-align: center; /* Centers the title */
        }

        #output {
            margin-bottom: 20px; /* Space below the output area */
            height: 200px; /* Fixed height for the output area */
            overflow-y: scroll; /* Scrolls if content overflows */
            border: 1px solid #ccc; /* Light gray border */
            padding: 10px; /* Padding inside the output area */
            background-color: #f9f9f9; /* Slightly darker gray background */
        }

        #input {
            width: calc(100% - 100px); /* Input field takes most of the width */
            padding: 10px; /* Padding inside the input field */
        }

        #submit {
            padding: 10px; /* Padding inside the submit button */
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>Text-Based Adventure Game</h1>
        <div id="output"></div> <!-- Area for displaying game output -->
        <input type="text" id="input" placeholder="Enter your action" /> <!-- Input for player actions -->
        <button id="submit">Submit</button> <!-- Button to submit actions -->
    </div>
    <script>
        // Base class for all characters
        class Character {
            // Constructor to initialize character properties
            constructor(name, health, attackPower) {
                this.name = name; // Character's name
                this.health = health; // Character's health
                this.attackPower = attackPower; // Character's attack power
            }

            // Method to perform an attack on a target character
            attack(target) {
                appendToOutput(`${this.name} attacks ${target.name} for ${this.attackPower} damage!`);
                target.takeDamage(this.attackPower); // Reduce the target's health
            }

            // Method for taking damage
            takeDamage(damage) {
                this.health -= damage; // Decrease health by damage amount
                appendToOutput(`${this.name} takes ${damage} damage and now has ${this.health} health left.`);
            }
        }

        // Warrior class inherits from Character
        class Warrior extends Character {
            // Warrior specific properties
            constructor(name) {
                super(name, 100, 15); // Warrior has 100 health and 15 attack power
            }

            // Overriding the attack method with a special message
            attack(target) {
                super.attack(target); // Call the parent class's attack method
                appendToOutput(`${this.name} strikes with great strength!`); // Additional message for Warrior's attack
            }
        }

        // Mage class inherits from Character
        class Mage extends Character {
            // Mage specific properties
            constructor(name) {
                super(name, 80, 20); // Mage has 80 health and 20 attack power
            }

            // Overriding the attack method with a special message
            attack(target) {
                super.attack(target); // Call the parent class's attack method
                appendToOutput(`${this.name} casts a powerful spell!`); // Additional message for Mage's attack
            }

            // Mage can heal themselves
            heal() {
                this.health += 10; // Increase health by 10
                appendToOutput(`${this.name} heals for 10 health and now has ${this.health} health.`);
            }
        }

        // Monster class to create monster characters
        class Monster {
            constructor(name, health, attackPower) {
                this.name = name; // Monster's name
                this.health = health; // Monster's health
                this.attackPower = attackPower; // Monster's attack power
            }

            // Monster's attack method
            attack(target) {
                appendToOutput(`${this.name} attacks ${target.name} for ${this.attackPower} damage!`);
                target.takeDamage(this.attackPower); // Reduce target's health
            }
        }

        // Array of character classes for player choice
        const characterClasses = ["Warrior", "Mage"];
        // Array of monsters with their names, health, and attack power
        const monsters = [
            new Monster("Goblin", 50, 10),
            new Monster("Orc", 60, 12)
        ];

        let player; // Variable to hold the player character
        let currentMonster; // Variable to hold the current monster

        // Start the game
        function startGame() {
            // Prompt for player name and character class
            const playerName = prompt("Enter your character's name:");
            const characterType = prompt(`Choose your character class (${characterClasses.join("/")})`).toLowerCase();

            // Instantiate player based on chosen class
            if (characterType === "warrior") {
                player = new Warrior(playerName); // Create a Warrior instance
            } else if (characterType === "mage") {
                player = new Mage(playerName); // Create a Mage instance
            } else {
                appendToOutput("Invalid character class. Defaulting to Warrior.");
                player = new Warrior(playerName); // Default to Warrior if input is invalid
            }

            // Randomly select a monster from the array
            currentMonster = monsters[Math.floor(Math.random() * monsters.length)];

            // Start the battle
            battle();
        }

        // Function to handle battle mechanics
        function battle() {
            appendToOutput(`A wild ${currentMonster.name} appears!`); // Introduce the monster
            const inputField = document.getElementById("input"); // Reference to input field
            const submitButton = document.getElementById("submit"); // Reference to submit button

            // On button click, process the player's action
            submitButton.onclick = () => {
                const action = inputField.value.toLowerCase(); // Get player input
                inputField.value = ""; // Clear the input for the next action

                // Check for player attack action
                if (action === "attack") {
                    player.attack(currentMonster); // Player attacks the monster
                } 
                // Check for healing action (only available for Mage)
                else if (action === "heal" && player instanceof Mage) {
                    player.heal(); // Player heals themselves
                } 
                // Invalid action handling
                else {
                    appendToOutput("Invalid action.");
                    return; // Skip turn if action is invalid
                }

                // Check if the monster is defeated
                if (currentMonster.health <= 0) {
                    appendToOutput(`Congratulations! ${player.name} has defeated the ${currentMonster.name}!`);
                    return; // End battle if monster is defeated
                }

                // Monster's turn to attack the player
                currentMonster.attack(player);

                // Check if player is defeated
                if (player.health <= 0) {
                    appendToOutput(`Game over! ${player.name} has been defeated by the ${currentMonster.name}.`);
                }
            };
        }

        // Function to append text to the output div
        function appendToOutput(text) {
            const output = document.getElementById("output"); // Reference to output area
            output.innerHTML += `<p>${text}</p>`; // Add new text to output area
            output.scrollTop = output.scrollHeight; // Auto-scroll to the bottom of output area
        }

        // Start the game when the page loads
        startGame(); // Call the function to initiate the game
    </script>
</body>
</html>
