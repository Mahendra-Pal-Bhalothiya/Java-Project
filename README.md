# Java-Project
import java.io.*;
import java.nio.file.*;
import java.util.Scanner;

public class firstProject{

    // Method to create or overwrite a file with text
    public static void writeFile(String fileName, String content) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName))) {
            writer.write(content);
            System.out.println("File written successfully.");
        } catch (IOException e) {
            System.out.println("Error writing to the file: " + e.getMessage());
        }
    }

    // Method to read the content of a file
    public static void readFile(String fileName) {
        try (BufferedReader reader = new BufferedReader(new FileReader(fileName))) {
            String line;
            System.out.println("\nReading the file content:");
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Error reading the file: " + e.getMessage());
        }
    }

    // Method to append text to an existing file
    public static void appendToFile(String fileName, String content) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName, true))) {
            writer.write(content);
            writer.newLine();  // Add a newline after appending
            System.out.println("Content appended successfully.");
        } catch (IOException e) {
            System.out.println("Error appending to the file: " + e.getMessage());
        }
    }

    // Method to modify specific content in the file
    public static void modifyFile(String fileName, String oldContent, String newContent) {
        try {
            // Read all content from the file
            Path path = Paths.get(fileName);
            String content = new String(Files.readAllBytes(path));

            // Replace old content with new content
            content = content.replace(oldContent, newContent);

            // Write the modified content back to the file
            Files.write(path, content.getBytes());
            System.out.println("File modified successfully.");
        } catch (IOException e) {
            System.out.println("Error modifying the file: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Ask user for the filename
        System.out.print("Enter the file name (including path if necessary): ");
        String fileName = scanner.nextLine();

        // Perform all operations on the file
        System.out.println("\nPerforming operations on the file: " + fileName);

        // Step 1: Write to file
        System.out.print("\nEnter the content to write to the file: ");
        String contentToWrite = scanner.nextLine();
        writeFile(fileName, contentToWrite);

        // Step 2: Read from file
        readFile(fileName);

        // Step 3: Append to file
        System.out.print("\nEnter the content to append to the file: ");
        String contentToAppend = scanner.nextLine();
        appendToFile(fileName, contentToAppend);

        // Step 4: Read again to show appended content
        readFile(fileName);

        // Step 5: Modify file content
        System.out.print("\nEnter the text to modify: ");
        String oldContent = scanner.nextLine();
        System.out.print("Enter the new content: ");
        String newContent = scanner.nextLine();
        modifyFile(fileName, oldContent, newContent);

        // Step 6: Read the file again to show modified content
        readFile(fileName);

        scanner.close();
    }
}
