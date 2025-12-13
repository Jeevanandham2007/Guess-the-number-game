# Guess-the-number-game
Here is a clear Java description for the “Guess the Number” game, writtenl for 5–10 or 16-mark answers):   ---  Guess the Number Game – Java Description  Guess the Number is a simple console-based Java game where the computer generates a random number and the player tries to guess it within a limited number of attempts.
import java.util.Scanner;
import java.util.Random;

public class GuessTheNumberGame {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        System.out.println("Welcome to the Guess The Number Game!");
        boolean playAgain = true;

        while (playAgain) {
            System.out.println("\nChoose difficulty level:");
            System.out.println("1 - Easy (1 to 50, 10 attempts)");
            System.out.println("2 - Medium (1 to 100, 7 attempts)");
            System.out.println("3 - Hard (1 to 200, 5 attempts)");
            System.out.print("Enter choice (1-3): ");

            int difficulty = 0;
            while (true) {
                if (scanner.hasNextInt()) {
                    difficulty = scanner.nextInt();
                    if (difficulty >= 1 && difficulty <= 3) break;
                    else System.out.print("Please enter a number between 1 and 3: ");
                } else {
                    System.out.print("Invalid input. Enter a number between 1 and 3: ");
                    scanner.next();
                }
            }

            int maxNumber = 50, maxAttempts = 10;
            switch (difficulty) {
                case 1:
                    maxNumber = 50;
                    maxAttempts = 10;
                    break;
                case 2:
                    maxNumber = 100;
                    maxAttempts = 7;
                    break;
                case 3:
                    maxNumber = 200;
                    maxAttempts = 5;
                    break;
            }

            int numberToGuess = random.nextInt(maxNumber) + 1;
            int attemptsLeft = maxAttempts;
            boolean guessedCorrectly = false;

            System.out.println("\nI've picked a number between 1 and " + maxNumber + ".");
            System.out.println("You have " + maxAttempts + " attempts to guess it. Good luck!");

            while (attemptsLeft > 0 && !guessedCorrectly) {
                System.out.print("\nEnter your guess: ");

                int guess;
                if (scanner.hasNextInt()) {
                    guess = scanner.nextInt();

                    if (guess < 1 || guess > maxNumber) {
                        System.out.println("Your guess must be between 1 and " + maxNumber + ". Try again.");
                        continue;
                    }

                    attemptsLeft--;

                    if (guess == numberToGuess) {
                        guessedCorrectly = true;
                        System.out.println("🎉 Congrats! You guessed the number!");
                        System.out.println("You used " + (maxAttempts - attemptsLeft) + " attempt(s).");
                    } else if (guess < numberToGuess) {
                        System.out.println("Too low! Attempts left: " + attemptsLeft);
                    } else {
                        System.out.println("Too high! Attempts left: " + attemptsLeft);
                    }

                } else {
                    System.out.println("Invalid input! Please enter an integer.");
                    scanner.next(); // clear invalid input
                }
            }

            if (!guessedCorrectly) {
                System.out.println("\nGame Over! The number was: " + numberToGuess);
            }

            System.out.print("\nDo you want to play again? (y/n): ");
            String response = scanner.next();
            playAgain = response.equalsIgnoreCase("y") || response.equalsIgnoreCase("yes");
        }

        System.out.println("\nThanks for playing! Goodbye!");
        scanner.close();
    }
}
