import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.*;

public class PasswordGeneratorGUI extends JFrame implements ActionListener {

    private static final String RECORDS_FILE = "records.txt";
    private static final String MAIN_USER = "admin";
    private static final String MAIN_PASSWORD = "password";

    private JLabel usernameLabel, passwordLengthLabel, passwordLabel;
    private JTextField usernameField, passwordLengthField, passwordField;
    private JButton generateButton;
    private JMenuBar menuBar;
    private JMenu fileMenu;
    private JMenuItem viewRecordsMenuItem;
    private JPasswordField mainPasswordField;

    public PasswordGeneratorGUI() {
        setTitle("Random Password Generator");
        setSize(400, 200);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(4, 2));

        usernameLabel = new JLabel("Username:");
        add(usernameLabel);
        usernameField = new JTextField();
        add(usernameField);

        passwordLengthLabel = new JLabel("Password Length:");
        add(passwordLengthLabel);
        passwordLengthField = new JTextField();
        add(passwordLengthField);

        passwordLabel = new JLabel("Password:");
        add(passwordLabel);
        passwordField = new JTextField();
        passwordField.setEditable(false);
        add(passwordField);

        generateButton = new JButton("Generate");
        generateButton.addActionListener(this);
        add(generateButton);

        menuBar = new JMenuBar();
        fileMenu = new JMenu("File");
        viewRecordsMenuItem = new JMenuItem("View Records");
        viewRecordsMenuItem.addActionListener(this);
        fileMenu.add(viewRecordsMenuItem);
        menuBar.add(fileMenu);
        setJMenuBar(menuBar);

        mainPasswordField = new JPasswordField();
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == generateButton) {
            String username = usernameField.getText();
            int passwordLength = Integer.parseInt(passwordLengthField.getText());

            String password = generatePassword(passwordLength);

            passwordField.setText(password);

            saveRecord(username, password);
        } else if (e.getSource() == viewRecordsMenuItem) {
            JPasswordField passwordField = new JPasswordField();
            int option = JOptionPane.showConfirmDialog(null, passwordField, "Enter main user password", JOptionPane.OK_CANCEL_OPTION, JOptionPane.PLAIN_MESSAGE);
            if (option == JOptionPane.OK_OPTION) {
                char[] password = passwordField.getPassword();
                if (verifyMainUserPassword(password)) {
                    viewRecords();
                } else {
                    JOptionPane.showMessageDialog(null, "Incorrect password", "Error", JOptionPane.ERROR_MESSAGE);
                }
                Arrays.fill(password, '0');
            }
        }
    }

    private String generatePassword(int length) {
        String characters = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+";
        StringBuilder sb = new StringBuilder();
        Random random = new Random();
        for (int i = 0; i < length; i++) {
            int index = random.nextInt(characters.length());
            sb.append(characters.charAt(index));
        }
        return sb.toString();
    }

    private void saveRecord(String username, String password) {
        try (FileWriter writer = new FileWriter(RECORDS_FILE, true)) {
            writer.write(username + "," + password + "\n");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private void viewRecords() {
        StringBuilder sb = new StringBuilder();
        try (Scanner scanner = new Scanner(new File(RECORDS_FILE))) {
            while (scanner.hasNextLine()) {
                String line = scanner.nextLine();
                sb.append(line).append("\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        JOptionPane.showMessageDialog(null, sb.toString(), "Records", JOptionPane.INFORMATION_MESSAGE);
    }
    public static void main(String[] args) {
    PasswordGeneratorGUI gui = new PasswordGeneratorGUI();
    gui.setVisible(true);
    }

    private boolean verifyMainUserPassword(char[] password) {
    return MAIN_USER.equals(usernameField.getText()) && Arrays.equals(password, MAIN_PASSWORD.toCharArray());
    }
}