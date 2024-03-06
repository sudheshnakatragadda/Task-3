import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class User {
    private String userId;
    private String pin;
    private double balance;
    private Map<Integer, Transaction> transactions;

    public User(String userId, String pin, double initialBalance) {
        this.userId = userId;
        this.pin = pin;
        this.balance = initialBalance;
        this.transactions = new HashMap<>();
    }

    public String getUserId() {
        return userId;
    }

    public String getPin() {
        return pin;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        balance += amount;
        addTransaction(TransactionType.DEPOSIT, amount);
    }

    public void withdraw(double amount) {
        if (amount > balance) {
            System.out.println("Insufficient funds!");
        } else {
            balance -= amount;
            addTransaction(TransactionType.WITHDRAW, amount);
        }
    }

    public void transfer(User recipient, double amount) {
        if (amount > balance) {
            System.out.println("Insufficient funds for transfer!");
        } else {
            balance -= amount;
            recipient.deposit(amount);
            addTransaction(TransactionType.TRANSFER, amount);
        }
    }

    public void displayTransactions() {
        System.out.println("Transaction History:");
        for (Map.Entry<Integer, Transaction> entry : transactions.entrySet()) {
            System.out.println(entry.getValue());
        }
    }

    private void addTransaction(TransactionType type, double amount) {
        int transactionId = transactions.size() + 1;
        Transaction transaction = new Transaction(transactionId, type, amount);
        transactions.put(transactionId, transaction);
    }
}

class Transaction {
    private int transactionId;
    private TransactionType type;
    private double amount;

    public Transaction(int transactionId, TransactionType type, double amount) {
        this.transactionId = transactionId;
        this.type = type;
        this.amount = amount;
    }

    @Override
    public String toString() {
        return "Transaction " + transactionId + ": " + type + " - $" + amount;
    }
}

enum TransactionType {
    DEPOSIT, WITHDRAW, TRANSFER
}

public class ATMSystem {
    private static Map<String, User> users = new HashMap<>();
    private static User currentUser;

    public static void main(String[] args) {
        initializeUsers();
        displayWelcomeScreen();
        authenticateUser();
        performOperations();
    }

    private static void initializeUsers() {
        users.put("user123", new User("user123", "1234", 1000.0));
        users.put("user456", new User("user456", "5678", 500.0));
    }

    private static void displayWelcomeScreen() {
        System.out.println("Welcome to the ATM System!");
    }

    private static void authenticateUser() {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.print("Enter User ID: ");
            String userId = scanner.nextLine();
            System.out.print("Enter PIN: ");
            String pin = scanner.nextLine();

            if (users.containsKey(userId) && users.get(userId).getPin().equals(pin)) {
                currentUser = users.get(userId);
                System.out.println("Authentication successful. Welcome, " + userId + "!");
                break;
            } else {
                System.out.println("Invalid User ID or PIN. Please try again.");
            }
        }
    }

    private static void performOperations() {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            displayMenu();
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    currentUser.displayTransactions();
                    break;
                case 2:
                    System.out.print("Enter withdrawal amount: $");
                    double withdrawalAmount = scanner.nextDouble();
                    currentUser.withdraw(withdrawalAmount);
                    break;
                case 3:
                    System.out.print("Enter deposit amount: $");
                    double depositAmount = scanner.nextDouble();
                    currentUser.deposit(depositAmount);
                    break;
                case 4:
                    System.out.print("Enter recipient User ID: ");
                    String recipientId = scanner.next();
                    System.out.print("Enter transfer amount: $");
                    double transferAmount = scanner.nextDouble();
                    User recipient = users.get(recipientId);
                    if (recipient != null) {
                        currentUser.transfer(recipient, transferAmount);
                    } else {
                        System.out.println("Recipient not found!");
                    }
                    break;
                case 5:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please choose again.");
            }
        }
    }

    private static void displayMenu() {
        System.out.println("\nATM Menu:");
        System.out.println("1. View Transactions History");
        System.out.println("2. Withdraw");
        System.out.println("3. Deposit");
        System.out.println("4. Transfer");
        System.out.println("5. Quit");
        System.out.print("Enter your choice: ");
    }
}
