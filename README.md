# Canteen.java
Canteen Ordering system
import java.util.Scanner;

public class Canteen {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        String[] menuItems = {"Champorado", "Egg Sandwich", "Pork Adobo", "Spaghetti", "Lumpia"};
        double[] menuPrices = {80.00, 50.00, 90.00, 70.00, 20.00};

        int totalQuantity = 0;
        double totalAmountBeforeDeduction = 0.0;
        double totalDeduction = 0.0;

        char orderAgain = 'Y';

        while (orderAgain == 'Y' || orderAgain == 'y') {
            System.out.println("\n----- MENU -----");
            for (int i = 0; i < menuItems.length; i++) {
                System.out.printf("%d. %-15s - $%.2f%n", (i + 1), menuItems[i], menuPrices[i]);
            }
            System.out.println();

            System.out.print("Enter item number: ");
            int itemNumber = scanner.nextInt();

            System.out.print("Enter quantity: ");
            int quantity = scanner.nextInt();

            if (itemNumber < 1 || itemNumber > 5 || quantity < 1 || quantity > 10) {
                System.out.println("\nInvalid order! Please enter a valid item and quantity.");
            } else {
                System.out.print("Are you a student? (Y/N): ");
                char isStudent = scanner.next().charAt(0);
                boolean studentStatus = (isStudent == 'Y' || isStudent == 'y');

                double itemPrice = menuPrices[itemNumber - 1];
                double subtotal = itemPrice * quantity;

                double discountRate = 0.0;
                if (studentStatus && subtotal >= 500) {
                    discountRate = 0.15;
                } else if (studentStatus) {
                    discountRate = 0.10;
                } else if (subtotal >= 500) {
                    discountRate = 0.05;
                }

                double discountAmount = subtotal * discountRate;
                double orderTotal = subtotal - discountAmount;

                System.out.println();
                System.out.printf("Subtotal: $%.2f%n", subtotal);
                System.out.printf("Discount: $%.2f%n", discountAmount);
                System.out.printf("Order total: $%.2f%n", orderTotal);

                totalQuantity += quantity;
                totalAmountBeforeDeduction += subtotal;
                totalDeduction += discountAmount;
            }

            System.out.println();
            System.out.print("Do you want to order again? (Y/N): ");
            orderAgain = scanner.next().charAt(0);
        }

        double finalAmountToPay = totalAmountBeforeDeduction - totalDeduction;

        System.out.println("\n=================================");
        System.out.println("        TRANSACTION SUMMARY      ");
        System.out.println("=================================");
        System.out.println("Total quantity of items purchased: " + totalQuantity);
        System.out.printf("Total amount before deductions: $%.2f%n", totalAmountBeforeDeduction);
        System.out.printf("Total deduction: $%.2f%n", totalDeduction);
        System.out.printf("Final amount to pay: $%.2f%n", finalAmountToPay);
        System.out.println("=================================");

        scanner.close();
    }
}
