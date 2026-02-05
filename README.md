import java.io.IOException;

public class LoginProgram {

    

    public static void main(String[] args) throws IOException {

        // Correct login details (for testing purpose)
        String correctUser = "admin";
        String correctPass = "1234";

        int triesLeft = 3;

        System.out.println("");
        System.out.println("        SYSTEM LOGIN PAGE         ");
        System.out.println("");

        // keep asking until attempts finish
        while (triesLeft > 0) {

            System.out.print("\nUsername: ");
            String userInput = readText();

            System.out.print("Password: ");
            String passInput = readHiddenPassword();

            // check if both username and password match
            if (userInput.equals(correctUser) && passInput.equals(correctPass)) {
                System.out.println("\nAccess granted. Login successful!");
                break; // exit loop if login works
            } 
            else {
                triesLeft--;
                System.out.println("\nWrong details entered.");

                if (triesLeft > 0) {
                    System.out.println("Please try again. Attempts remaining: " + triesLeft);
                } else {
                    System.out.println("No attempts left. Access denied.");
                }
            }
        }
    }

    // method for reading normal input like username
    public static String readText() throws IOException {
        StringBuilder text = new StringBuilder();
        int ch;

        while ((ch = System.in.read()) != '\n') {
            if (ch != '\r') {
                text.append((char) ch);
            }
        }
        return text.toString();
    }

    // method for reading password and showing * instead of characters
    public static String readHiddenPassword() throws IOException {
        StringBuilder password = new StringBuilder();
        int ch;

        while ((ch = System.in.read()) != '\n') {

            if (ch == '\r') continue;

            // handle backspace if user deletes a character
            if (ch == 8 || ch == 127) {
                if (password.length() > 0) {
                    password.deleteCharAt(password.length() - 1);
                    System.out.print("\b \b");
                }
            } 
            else {
                password.append((char) ch);
                System.out.print("*");
            }
        }

        return password.toString();
    }
}
