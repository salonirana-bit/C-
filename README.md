#include <iostream>
#include <random>
#include <cctype>

// Using constants to represent game choices
const char ROCK = 'r';
const char PAPER = 'p';
const char SCISSORS = 's';

// Function prototypes
char getComputerChoice();
char getUserChoice();
void showChoice(char choice);
void chooseWinner(char player, char computer);

int main() {
    char playAgain;
    
    std::cout << "====================================\n";
    std::cout << " Welcome to Rock, Paper, Scissors! \n";
    std::cout << "====================================\n";

    do {
        char player = getUserChoice();
        std::cout << "\nYou chose: ";
        showChoice(player);

        char computer = getComputerChoice();
        std::cout << "Computer chose: ";
        showChoice(computer);

        chooseWinner(player, computer);

        std::cout << "\nDo you want to play another round? (y/n): ";
        std::cin >> playAgain;
        playAgain = std::tolower(playAgain);
        std::cout << "\n";

    } while (playAgain == 'y');

    std::cout << "Thanks for playing! Goodbye.\n";
    return 0;
}

// Generates a random choice for the computer using modern <random> library
char getComputerChoice() {
    // Initialize random number engine
    std::random_device rd; 
    std::mt19937 gen(rd()); 
    std::uniform_int_distribution<> distrib(1, 3); 

    int randomNum = distrib(gen);

    switch (randomNum) {
        case 1: return ROCK;
        case 2: return PAPER;
        case 3: return SCISSORS;
        default: return ROCK;
    }
}

// Prompts user for their move and enforces input validation
char getUserChoice() {
    char choice;
    do {
        std::cout << "Enter your choice:\n";
        std::cout << " '" << ROCK << "' for Rock\n";
        std::cout << " '" << PAPER << "' for Paper\n";
        std::cout << " '" << SCISSORS << "' for Scissors\n";
        std::cout << "Choice: ";
        std::cin >> choice;
        
        choice = std::tolower(choice); // Handle uppercase inputs gracefully

        if (choice != ROCK && choice != PAPER && choice != SCISSORS) {
            std::cout << "Invalid input. Please try again.\n\n";
        }
    } while (choice != ROCK && choice != PAPER && choice != SCISSORS);

    return choice;
}

// Maps the character choice to a readable text representation
void showChoice(char choice) {
    switch (choice) {
        case ROCK: std::cout << "Rock \n"; break;
        case PAPER: std::cout << "Paper \n"; break;
        case SCISSORS: std::cout << "Scissors \n"; break;
    }
}

// Evaluates the moves according to the game rules and announces the outcome
void chooseWinner(char player, char computer) {
    if (player == computer) {
        std::cout << "It's a tie! \n";
    } 
    else if ((player == ROCK && computer == SCISSORS) ||
             (player == PAPER && computer == ROCK) ||
             (player == SCISSORS && computer == PAPER)) {
        std::cout << "Congratulations! You win! \n";
    } 
    else {
        std::cout << "Oh no! You lose. 🤖 wins!\n";
    }
}
