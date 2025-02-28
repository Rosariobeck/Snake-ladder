# Snake-ladder

import java.util.*;
public class MyClass {
public static void main(String args[]) {
    Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        int player1Position = 0;
        int player2Position = 0;

        System.out.print("Enter Player 1's name: ");
        String player1Name = scanner.nextLine();

        System.out.print("Enter Player 2's name: ");
        String player2Name = scanner.nextLine();

        System.out.println("Let's start the game!");

        while (player1Position < 100 && player2Position < 100) {
            player1Position = playTurn(player1Name, player1Position, random);
            if (player1Position >= 100) {
                System.out.println(player1Name + " wins!");
                break;
            }

            player2Position = playTurn(player2Name, player2Position, random);
            if (player2Position >= 100) {
                System.out.println(player2Name + " wins!");
                break;
            }
        }
        scanner.close();
  }
  
   public static int playTurn(String playerName, int position, Random random) {
        System.out.println("\n" + playerName + "'s turn.");
        int diceRoll = random.nextInt(6) + 1;
        System.out.println(playerName + " rolled a " + diceRoll);

        position += diceRoll;

        if (position > 100) {
            position -= diceRoll;
            System.out.println("Cannot move. You need exactly " + (100 - position) + " to win.");
            return position;
        }

        position = checkSnakesAndLadders(position);
        System.out.println(playerName + " is now at position " + position);

        return position;
    }

    public static int checkSnakesAndLadders(int position) {
        Map<Integer, Integer> snakesAndLadders = new HashMap<>();

        // Snakes
        snakesAndLadders.put(99, 41);
        snakesAndLadders.put(95, 56);
        snakesAndLadders.put(87, 17);
        snakesAndLadders.put(62, 19);
        snakesAndLadders.put(54, 34);
        snakesAndLadders.put(52, 11);
        snakesAndLadders.put(25, 4);

        // Ladders
        snakesAndLadders.put(2, 38);
        snakesAndLadders.put(8, 31);
        snakesAndLadders.put(28, 84);
        snakesAndLadders.put(21, 42);
        snakesAndLadders.put(51, 67);
        snakesAndLadders.put(71, 91);
        snakesAndLadders.put(80, 100);

        if (snakesAndLadders.containsKey(position)) {
            int newPosition = snakesAndLadders.get(position);
            System.out.println((newPosition < position ? "Snake bite! " : "Ladder climb! ") + "Moved to " + newPosition + ".");
            return newPosition;
        }
        return position;
    }
}
