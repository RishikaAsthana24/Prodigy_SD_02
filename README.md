import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;

public class Main {
    private int numberToGuess;
    private int numberOfAttempts;

    public Main() {
        Random random = new Random();
        numberToGuess = random.nextInt(100) + 1;
        numberOfAttempts = 0;

        JFrame frame = new JFrame("Guessing Game");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 200);

        JPanel panel = new JPanel();
        frame.add(panel);
        placeComponents(panel);

        frame.setVisible(true);
    }

    private void placeComponents(JPanel panel) {
        panel.setLayout(null);

        JLabel userLabel = new JLabel("Enter your guess:");
        userLabel.setBounds(10, 20, 150, 25);
        panel.add(userLabel);

        JTextField userText = new JTextField(20);
        userText.setBounds(150, 20, 165, 25);
        panel.add(userText);

        JButton guessButton = new JButton("Guess");
        guessButton.setBounds(10, 80, 150, 25);
        panel.add(guessButton);

        JLabel feedbackLabel = new JLabel("");
        feedbackLabel.setBounds(10, 110, 300, 25);
        panel.add(feedbackLabel);

        guessButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String userInput = userText.getText();
                try {
                    int guess = Integer.parseInt(userInput);
                    numberOfAttempts++;
                    if (guess < numberToGuess) {
                        feedbackLabel.setText("Too low! Try again.");
                    } else if (guess > numberToGuess) {
                        feedbackLabel.setText("Too high! Try again.");
                    } else {
                        feedbackLabel.setText("Correct! You took " + numberOfAttempts + " attempts.");
                       int playAgain = JOptionPane.showConfirmDialog(null, "You won! Play again?", "Play Again", JOptionPane.YES_NO_OPTION);
                      if (playAgain == JOptionPane.YES_OPTION) {
                           resetGame();
                            feedbackLabel.setText("");
                          userText.setText("");
                      } else {
                           System.exit(0);
                       }
                    }
              } catch (NumberFormatException ex) {
                    feedbackLabel.setText("Please enter a valid number.");
                }
            }
        });
    }

    private void resetGame() {
        Random random = new Random();
        numberToGuess = random.nextInt(100) + 1;
        numberOfAttempts = 0;
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new Main();
            }
        });
    }
}
