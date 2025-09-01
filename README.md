# exceptionhandlinginjava
import java.util.Scanner;
public class Eceptionhandling {
    
   /**
     * Method that demonstrates throwing checked exceptions
     * InterruptedException is a checked exception that must be declared in method signature
     * 
     * @param sec number of seconds to wait
     * @throws InterruptedException if the thread is interrupted while sleeping
     */
    static void waitforseconds(int sec) throws InterruptedException {
        System.out.println("waiting " + sec + " seconds...");
        // Thread.sleep() can throw InterruptedException - a checked exception
        Thread.sleep(sec * 1000); // Convert seconds to milliseconds
        System.out.println("waiting done");
    }

  public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
  // ===== TRY-CATCH-FINALLY BLOCK DEMONSTRATION =====
        // try: Contains code that might throw an exception
        // catch: Handles specific types of exceptions
        // finally: Always executes, regardless of whether exception occurs
        try {
            System.out.println("enter the numerator:");
            int a = sc.nextInt(); // Could throw InputMismatchException if non-integer entered
            System.out.print("enter the denominator:");
            int b = sc.nextInt(); // Could throw InputMismatchException if non-integer entered
            
   // This line could throw ArithmeticException if b is 0 (division by zero)
            int result = a / b;
            System.out.println("result = " + result);
        }
        // SPECIFIC EXCEPTION HANDLING: Catch ArithmeticException first
        // More specific exceptions should be caught before general ones
        catch(ArithmeticException e) {
            System.out.println("error: division by zero is not allowed!");
            // 'e' contains details about the exception that occurred
        }
        // GENERAL EXCEPTION HANDLING: Catch any other type of exception
        // This acts as a "catch-all" for any exceptions not caught above
        catch (Exception e) {
            System.out.println("some other error: " + e);
            // This will catch InputMismatchException, NumberFormatException, etc.
        }
        // FINALLY BLOCK: Always executes whether exception occurs or not
        // Used for cleanup operations like closing files, database connections, etc.
        finally {
            System.out.println("finally block: ye hamesha chalega!");
            // This block runs even if an exception occurs and is caught
        }

  // ===== MANUAL EXCEPTION THROWING DEMONSTRATION =====
        // Sometimes we need to throw exceptions manually based on business logic
        System.out.println("enter your age:");
        int age = sc.nextInt();
        
  // Custom validation: throw exception if age requirement not met
        if (age < 18) {
            // THROW STATEMENT: Manually throwing an exception
            // We're using ArithmeticException here, but in real projects you'd create custom exceptions
            throw new ArithmeticException("not eligible for voting (age < 18)");
        }
        else {
            System.out.println("eligible for voting!");
        }
        
  System.out.println("program ended successfully!");
        // RESOURCE CLEANUP: Close Scanner to prevent resource leaks
        // In real applications, this should be in a finally block or use try-with-resources
        sc.close();
    }
}

/*
 * KEY EXCEPTION HANDLING CONCEPTS DEMONSTRATED:
 * 
 * 1. CHECKED vs UNCHECKED EXCEPTIONS:
 *    - Checked: Must be declared in method signature (like InterruptedException)
 *    - Unchecked: Runtime exceptions (like ArithmeticException, InputMismatchException)
 * 
 * 2. EXCEPTION HIERARCHY:
 *    - Exception (general) -> ArithmeticException (specific)
 *    - Always catch specific exceptions before general ones
 * 
 * 3. TRY-CATCH-FINALLY FLOW:
 *    - try: Code that might fail
 *    - catch: Handle the failure
 *    - finally: Cleanup code (always runs)
 * 
 * 4. THROWING EXCEPTIONS:
 *    - Use 'throw' keyword to manually throw exceptions
 *    - Useful for business logic validation
 * 
 * 5. BEST PRACTICES:
 *    - Handle specific exceptions appropriately
 *    - Use finally for cleanup operations
 *    - Don't ignore exceptions (empty catch blocks)
 *    - Log exception details for debugging
 */
