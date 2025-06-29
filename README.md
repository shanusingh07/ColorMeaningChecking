# ColorMeaningChecking
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class colorMeaningChecker {
    private static final Map<String, String> colorMeanings = new HashMap<>();
    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        initializeColorMeanings();
        displayWelcomeMessage();

        while (true) {
            displayMainMenu();
            String choice = scanner.nextLine().trim();

            switch (choice) {
                case "1":
                    checkColorMeaning();
                    break;
                case "2":
                    addNewColor();
                    break;
                case "3":
                    listAllColors();
                    break;
                case "4":
                    System.out.println("\nThank you for using the Color Meaning Checker. Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("\nInvalid option. Please try again.");
            }
        }
    }

    private static void initializeColorMeanings() {
        colorMeanings.put("RED", "Symbolizes passion, energy, love, and danger");
        colorMeanings.put("BLUE", "Represents calmness, trust, loyalty, and stability");
        colorMeanings.put("GREEN", "Signifies nature, growth, harmony, and renewal");
        colorMeanings.put("YELLOW", "Represents happiness, optimism, creativity, and warmth");
        colorMeanings.put("PURPLE", "Symbolizes luxury, power, ambition, and mystery");
        colorMeanings.put("ORANGE", "Represents enthusiasm, excitement, and success");
        colorMeanings.put("PINK", "Symbolizes romance, compassion, and playfulness");
        colorMeanings.put("BLACK", "Represents power, elegance, mystery, and the unknown");
        colorMeanings.put("WHITE", "Symbolizes purity, innocence, cleanliness, and new beginnings");
    }

    private static void displayWelcomeMessage() {
        System.out.println("🌈 Welcome to the Color Meaning Checker! 🌈");
        System.out.println("Discover the symbolism and meanings behind different colors.");
    }

    private static void displayMainMenu() {
        System.out.println("\nMain Menu:");
        System.out.println("1. Check color meaning");
        System.out.println("2. Add a new color meaning");
        System.out.println("3. List all available colors");
        System.out.println("4. Exit");
        System.out.print("Enter your choice (1-4): ");
    }

    private static void checkColorMeaning() {
        System.out.print("\nEnter a color name: ");
        String colorName = scanner.nextLine().trim().toUpperCase();

        if (colorName.isEmpty()) {
            System.out.println("Error: Color name cannot be empty. Please try again.");
            return;
        }

        if (colorMeanings.containsKey(colorName)) {
            System.out.println("\nColor Meaning for " + colorName + ":");
            System.out.println(colorMeanings.get(colorName));
        } else {
            System.out.println("\nColor not found in our database. Would you like to:");
            System.out.println("1. Try another color");
            System.out.println("2. Add this color to our database");
            System.out.print("Enter your choice (1-2): ");
            
            String option = scanner.nextLine().trim();
            if (option.equals("2")) {
                addNewColor(colorName);
            }
        }
    }

    private static void addNewColor() {
        System.out.print("\nEnter the new color name: ");
        String colorName = scanner.nextLine().trim().toUpperCase();

        if (colorName.isEmpty()) {
            System.out.println("Error: Color name cannot be empty.");
            return;
        }

        addNewColor(colorName);
    }

    private static void addNewColor(String colorName) {
        if (colorMeanings.containsKey(colorName)) {
            System.out.println("\nThis color already exists in our database.");
            System.out.println("Current meaning: " + colorMeanings.get(colorName));
            System.out.print("Would you like to update it? (yes/no): ");
            String response = scanner.nextLine().trim().toLowerCase();
            
            if (!response.equals("yes")) {
                return;
            }
        }

        System.out.print("Enter the meaning for " + colorName + ": ");
        String meaning = scanner.nextLine().trim();

        if (meaning.isEmpty()) {
            System.out.println("Error: Meaning cannot be empty.");
            return;
        }

        colorMeanings.put(colorName, meaning);
        System.out.println("\nSuccessfully " + (colorMeanings.containsKey(colorName) ? "updated" : "added") + 
                         " the color " + colorName + "!");
    }

    private static void listAllColors() {
        System.out.println("\nAvailable Colors in Our Database:");
        System.out.println("--------------------------------");
        
        for (String color : colorMeanings.keySet()) {
            System.out.println("- " + color);
        }
        
        System.out.println("\nTotal colors: " + colorMeanings.size());
        System.out.println("\nEnter any color name to see its meaning, or 'back' to return to menu.");
        System.out.print("Your choice: ");
        
        String input = scanner.nextLine().trim().toUpperCase();
        if (!input.equals("BACK")) {
            checkColorMeaning(input);
        }
    }

    private static void checkColorMeaning(String colorName) {
        if (colorMeanings.containsKey(colorName)) {
            System.out.println("\nColor Meaning for " + colorName + ":");
            System.out.println(colorMeanings.get(colorName));
        } else {
            System.out.println("\nColor not found. Would you like to add it? (yes/no): ");
            String response = scanner.nextLine().trim().toLowerCase();
            
            if (response.equals("yes")) {
                addNewColor(colorName);
            }
        }
    }
}


