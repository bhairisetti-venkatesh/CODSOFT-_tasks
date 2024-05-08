import java.util.Scanner;

 class ATM {
  
  private UserAccount userAccount;
  private int mAttempts = 3;
  private int pAttempts = 0;

  public ATM(UserAccount userAccount) {
    this.userAccount = userAccount;
  }

  public void start() {
    Scanner scanner = new Scanner(System.in);
System.out.println("Welcome to the ATM!");
    while (true) {
      
      System.out.println("Please select an option:");
      System.out.println("1. Withdraw");
      System.out.println("2. Deposit");
      System.out.println("3. Balance Enquiry");
      System.out.println("4. Exit");

      int choice = scanner.nextInt();

      switch (choice) {
        case 1:
          withdraw();
          break;
        case 2:
          deposit();
          break;
        case 3:
          checkBalance();
          break;
        case 4:
          System.exit(0);
        default:
          System.out.println("Invalid option");
      }
    }
  }

  private void withdraw() {
    Scanner scanner = new Scanner(System.in);
   
   

    while (pAttempts < mAttempts) {
      System.out.println("Enter the withdrawal amount");
      int amount = scanner.nextInt();

      if (userAccount.getBalance() >= amount) {
        userAccount.withdraw(amount);
        System.out.println("Please collect your cash.");
        System.out.println("Transaction successful!");
        break; 
      } else {
        System.out.println("Insufficient balance.");
        pAttempts++;
      }
    }

    if (pAttempts == mAttempts) {
      System.out.println("You have reached the maximum limit attempts!.");
    }
  }

  private void deposit() {
    Scanner scanner = new Scanner(System.in);

    System.out.println("Enter the amount you want to deposit:");
    int amount = scanner.nextInt();

    userAccount.deposit(amount);
    System.out.println("Your deposit was successful.");
    System.out.println("Transaction successful!");
  }

  private void checkBalance() {
    System.out.println("Your balance is: " + userAccount.getBalance());
    System.out.println("Transaction successful!");
  }
  
  private void checkBalanceWithMessage() {
    int balance = userAccount.getBalance();
    if (balance < 1000) {
      System.out.println("Your current account balance is low!!");
    } else {
      System.out.println("Your balance is: " + balance);
    }
  }
}


 class UserAccount {
  
  private int balance;
  
  public UserAccount(int balance) {
    this.balance = balance;
  }
  
  public int getBalance() {
    return balance;
  }
  
  public void withdraw(int amount) {
    balance -= amount;
  }
  
  public void deposit(int amount) {
    balance += amount;
  }
}


public class Main {
  
  public static void main(String[] args) {
    UserAccount userAccount = new UserAccount(10000);
    ATM atm = new ATM(userAccount);
    
    atm.start();
  }
