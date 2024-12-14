# CS61A: Hog

This repository contains the implementation of the Hog project for UC Berkeley's CS61A course. Hog is a dice game simulation designed to teach students foundational programming concepts such as control structures, higher-order functions, and strategic game design.

## Project Overview
In Hog, two players take turns rolling dice to earn points. The goal is to be the first to score 100 points or more. However, several unique rules and mechanics make the game more interesting and strategic. This project involves implementing the game's logic, special rules, and a basic player interface.

### Key Concepts
- **Higher-order functions**: Functions that take other functions as arguments or return functions.
- **Control flow**: Implementing game rules with conditionals and loops.
- **Simulation**: Simulating multiple games to analyze strategies.

## Repository Structure
```
cs61a-hog/
├── hog.py           # Main game logic and rules implementation
├── dice.py          # Dice-rolling functions and utilities
├── hog_gui.py       # Graphical User Interface for playing Hog
├── tests/           # Directory containing test files
└── README.md        # Project overview and instructions (this file)
```

## Getting Started

### Prerequisites
To run the project, you'll need Python 3.6 or later. Install it from the [official Python website](https://www.python.org/downloads/).

### Installation
Clone the repository:
```bash
git clone https://github.com/matthewtridoan/cs61a-hog.git
cd cs61a-hog
```

### Running the Game
To play Hog with the graphical interface:
```bash
python hog_gui.py
```

## Rules of the Game
In Hog, two players alternate turns trying to be the first to end a turn with at least GOAL total points, where GOAL defaults to 100. On each turn, the current player chooses some number of dice to roll together, up to 10. That player's score for the turn is the sum of the dice outcomes. However, a player who rolls too many dice risks:

### Sow Sad
If any of the dice outcomes is a 1, the current player's score for the turn is 1, regardless of the other values rolled.

- **Example 1**: The current player rolls 7 dice, 5 of which are 1's. They score 1 point for the turn.
- **Example 2**: The current player rolls 4 dice, all of which are 3's. Since Sow Sad did not occur, they score 12 points for the turn.

In a normal game of Hog, those are all the rules. To spice up the game, we'll include some special rules:

### Boar Brawl
A player who chooses to roll zero dice scores three times the absolute difference between the tens digit of the opponent’s score and the ones digit of the current player’s score, or 1, whichever is greater. The ones digit refers to the rightmost digit and the tens digit refers to the second-rightmost digit. If a player's score is a single digit (less than 10), the tens digit of that player's score is 0.

- **Example 1**: The current player has 21 points and the opponent has 46 points, and the current player chooses to roll zero dice. The tens digit of the opponent's score is 4 and the ones digit of the current player's score is 1. Therefore, the player gains 3 * abs(4 - 1) = 9 points.
- **Example 2**: The current player has 45 points and the opponent has 52 points, and the current player chooses to roll zero dice. The tens digit of the opponent's score is 5 and the ones digit of the current player's score is 5. Since 3 * abs(5 - 5) = 0, the player gains 1 point.
- **Example 3**: The current player has 2 points and the opponent has 5 points, and the current player chooses to roll zero dice. The tens digit of the opponent's score is 0 and the ones digit of the current player's score is 2. Therefore, the player gains 3 * abs(0 - 2) = 6 points.

### Sus Fuss
We call a number sus if it has exactly 3 or 4 factors, including 1 and the number itself. If, after rolling, the current player's score is a sus number, their score instantly increases to the next prime number.

- **Example 1**: A player has 14 points and rolls 2 dice that earns them 7 points. Their new score would be 21, which has 4 factors: 1, 3, 7, and 21. Therefore, 21 is sus, and the player's score is immediately increased to 23, the next prime number.
- **Example 2**: A player with 63 points rolls 5 dice and earns 1 point from their turn. Their new score would be 64 (Sow Sad 😢), which has 7 factors: 1, 2, 4, 8, 16, 32, and 64. Since 64 is not sus, the score of the player is unchanged.
- **Example 3**: A player has 49 points and rolls 5 dice that total 18 points. Their new score would be 67, which is prime and has 2 factors: 1 and 67. Since 67 is not sus, the score of the player is unchanged.

## Contributing
Contributions are welcome! If you'd like to make changes or improvements, feel free to fork the repository, make your changes, and submit a pull request.

## Acknowledgments
- **UC Berkeley CS61A Team**: For creating this fantastic project.
- **John DeNero**: Instructor of CS61A, whose materials inspired this implementation.
- [CS61A Official Website](https://cs61a.org/): Course resources and materials.
