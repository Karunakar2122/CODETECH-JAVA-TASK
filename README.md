# CODETECH-JAVA-TASK
# Tic-Tac-Toe Game Documentation

## Overview
This Java program implements a text-based Tic-Tac-Toe game where two players, one human and one computer, take turns placing their marks on a 3x3 grid. The game checks for wins, draws, and handles invalid moves.

## Functions

### printBoard
- **Description**: Prints the current state of the game board.
- **Parameters**: 
  - `board`: The current game board represented as a 2D array of characters.
- **Output**: Prints the board to the console.

### checkWinner
- **Description**: Checks if a player has won the game.
- **Parameters**: 
  - `board`: The current game board represented as a 2D array of characters.
  - `player`: The player ('X' or 'O') whose win is being checked.
- **Returns**: True if the player has won, false otherwise.

### checkDraw
- **Description**: Checks if the game has ended in a draw.
- **Parameters**: 
  - `board`: The current game board represented as a 2D array of characters.
- **Returns**: True if the game is a draw, false otherwise.

### getPlayerMove
- **Description**: Gets the player's move.
- **Parameters**: 
  - `board`: The current game board represented as a 2D array of characters.
  - `player`: The player ('X' or 'O') who is making the move.
- **Input**: Prompts the player to enter their move (row and column).
- **Behavior**: Validates the move and updates the board accordingly.

### getComputerMove
- **Description**: Gets the computer's move (randomly).
- **Parameters**: 
  - `board`: The current game board represented as a 2D array of characters.
  - `player`: The player ('X' or 'O') for the computer.
- **Behavior**: Generates a random move for the computer and updates the board.

### main
- **Description**: Main function to start the Tic-Tac-Toe game.
- **Flow**: 
  - Initializes the game board and starting player.
  - Displays the initial state of the board.
  - Enters a loop where players take turns making moves until a winner is determined or the game ends in a draw.

## Usage
Compile and run the Java program. Follow the prompts to input your moves. The game will display the current state of the board after each move and inform you of the result (win, draw, or ongoing) at the end.

import java.util.Random;
import java.util.Scanner;

public class TicTacToe {

    /**
     * Function to print the current state of the board.
     * @param board The current game board represented as a 2D array of characters.
     */
    public static void printBoard(char[][] board) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j]);
                if (j < 2)
                    System.out.print(" | ");
            }
            System.out.println();
            if (i < 2)
                System.out.println("---------");
        }
    }

    /**
     * Function to check if a player has won.
     * @param board The current game board represented as a 2D array of characters.
     * @param player The player ('X' or 'O') whose win is being checked.
     * @return True if the player has won, false otherwise.
     */
    public static boolean checkWinner(char[][] board, char player) {
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == player && board[i][1] == player && board[i][2] == player) // Check rows
                return true;
            if (board[0][i] == player && board[1][i] == player && board[2][i] == player) // Check columns
                return true;
        }
        if (board[0][0] == player && board[1][1] == player && board[2][2] == player) // Check diagonal \
            return true;
        if (board[0][2] == player && board[1][1] == player && board[2][0] == player) // Check diagonal /
            return true;
        return false;
    }

    /**
     * Function to check if the game is a draw.
     * @param board The current game board represented as a 2D array of characters.
     * @return True if the game is a draw, false otherwise.
     */
    public static boolean checkDraw(char[][] board) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ')
                    return false; // If any cell is empty, the game is not a draw
            }
        }
        return true; // If all cells are filled and there's no winner, the game is a draw
    }

    /**
     * Function to get the player's move.
     * @param board The current game board represented as a 2D array of characters.
     * @param player The player ('X' or 'O') who is making the move.
     */
    public static void getPlayerMove(char[][] board, char player) {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.print("Enter your move (row column): ");
            int row = scanner.nextInt();
            int col = scanner.nextInt();
            if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
                board[row][col] = player;
                break;
            } else {
                System.out.println("Invalid move. Please try again.");
            }
        }
    }

    /**
     * Function to get the computer's move (random).
     * @param board The current game board represented as a 2D array of characters.
     * @param player The player ('X' or 'O') for the computer.
     */
    public static void getComputerMove(char[][] board, char player) {
        Random random = new Random();
        while (true) {
            int row = random.nextInt(3);
            int col = random.nextInt(3);
            if (board[row][col] == ' ') {
                board[row][col] = player;
                System.out.println("Computer chooses position: " + row + " " + col);
                break;
            }
        }
    }

    /**
     * Main function to start the Tic-Tac-Toe game.
     */
    public static void main(String[] args) {
        char[][] board = new char[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' '; // Initialize the board with empty cells
            }
        }

        char[] players = {'X', 'O'};
        int currentPlayerIndex = new Random().nextInt(2); // Randomly choose the starting player
        char currentPlayer = players[currentPlayerIndex];

        System.out.println("Welcome to Tic-Tac-Toe!");
        printBoard(board);

        while (true) {
            if (currentPlayer == 'X') {
                getPlayerMove(board, currentPlayer);
            } else {
                getComputerMove(board, currentPlayer);
            }
            printBoard(board);

            if (checkWinner(board, currentPlayer)) {
                System.out.println("Player " + currentPlayer + " wins!");
                break;
            }
            if (checkDraw(board)) {
                System.out.println("It's a draw!");
                break;
            }
            // Switch to the other player
            currentPlayerIndex = (currentPlayerIndex + 1) % 2;
            currentPlayer = players[currentPlayerIndex];
        }
    }
}
