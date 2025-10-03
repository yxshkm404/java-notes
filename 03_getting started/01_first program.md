# First Java Program - Hello World

## Introduction

Every programmer's journey begins with the classic "Hello World" program. This simple program introduces you to the basic structure and syntax of Java while demonstrating how to display output on the screen.

![Java Hello World](https://raw.githubusercontent.com/github/explore/5b3600551e122a3277c2c5368af2ad5725ffa9a1/topics/java/java.png)

## Your First Java Program

Let's start with the complete "Hello World" program:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

When you run this program, it will display:
```
Hello, World!
```

## Understanding the Program Structure

Let's break down each component of this program to understand what every line does.

### 1. Class Declaration

```java
public class HelloWorld {
    // class body
}
```

- **`public`**: An access modifier that makes this class accessible from anywhere
- **`class`**: A keyword that declares a class in Java
- **`HelloWorld`**: The name of our class (must match the filename: `HelloWorld.java`)
- **`{}`**: Curly braces define the class body - everything inside belongs to this class

**Important Rules:**
- Class names should start with a capital letter (PascalCase)
- The filename must match the public class name exactly
- Java is case-sensitive: `HelloWorld` ≠ `helloworld`

### 2. The main Method

```java
public static void main(String[] args) {
    // method body
}
```

This is the entry point of any Java application. Let's understand each keyword:

- **`public`**: Makes the method accessible from anywhere (JVM needs to access it)
- **`static`**: Allows the method to be called without creating an object of the class
- **`void`**: Indicates that this method doesn't return any value
- **`main`**: The specific name that JVM looks for when starting the program
- **`String[] args`**: Parameter that accepts command-line arguments as an array of Strings

**Note:** The main method signature must be exactly as shown. Even a small change will prevent your program from running.

### 3. The Print Statement

```java
System.out.println("Hello, World!");
```

This line actually prints the output:

- **`System`**: A built-in Java class that provides access to system resources
- **`out`**: A static field in System class representing standard output stream (console)
- **`println`**: A method that prints the text and adds a new line
- **`"Hello, World!"`**: The string (text) to be printed
- **`;`**: Semicolon marks the end of a statement (mandatory in Java)

## Complete Program Walkthrough

Here's the complete program with detailed comments:

```java
// This is a single-line comment
/* This is a
   multi-line comment */

/**
 * This is a documentation comment (Javadoc)
 * It's used to generate documentation for your code
 */
public class HelloWorld {                    // Class declaration
    public static void main(String[] args) { // Main method - program entry point
        System.out.println("Hello, World!"); // Print statement
    }                                        // End of main method
}                                            // End of class
```

## How to Run the Program

### Step 1: Create the Java File

Create a file named `HelloWorld.java` with the program code:

```bash
# Using command line
echo 'public class HelloWorld { public static void main(String[] args) { System.out.println("Hello, World!"); } }' > HelloWorld.java

# Or use any text editor
notepad HelloWorld.java  # Windows
nano HelloWorld.java     # Linux/Mac
```

### Step 2: Compile the Program

```bash
javac HelloWorld.java
```

This creates a `HelloWorld.class` file containing bytecode.

### Step 3: Run the Program

```bash
java HelloWorld
```

Output:
```
Hello, World!
```

## Variations of Hello World

### 1. Multiple Print Statements

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        System.out.println("Welcome to Java Programming!");
        System.out.println("This is my first program.");
    }
}
```

Output:
```
Hello, World!
Welcome to Java Programming!
This is my first program.
```

### 2. Using print vs println

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.print("Hello, ");    // Doesn't add new line
        System.out.print("World!");      // Continues on same line
        System.out.println();            // Just adds a new line
        System.out.println("New line");  // Prints and adds new line
    }
}
```

Output:
```
Hello, World!
New line
```

### 3. Using Escape Sequences

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello\tWorld!");      // Tab
        System.out.println("Hello\nWorld!");      // New line
        System.out.println("Hello \"World\"!");   // Double quotes
        System.out.println("Hello \'World\'!");   // Single quotes
        System.out.println("Hello\\World!");      // Backslash
    }
}
```

Output:
```
Hello   World!
Hello
World!
Hello "World"!
Hello 'World'!
Hello\World!
```

### 4. Using printf for Formatted Output

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.printf("Hello, %s!%n", "World");
        System.out.printf("The year is %d%n", 2024);
        System.out.printf("Pi is approximately %.2f%n", 3.14159);
    }
}
```

Output:
```
Hello, World!
The year is 2024
Pi is approximately 3.14
```

## Common Mistakes and Solutions

### 1. Incorrect Class Name

❌ **Wrong:**
```java
public class helloworld {  // Filename: HelloWorld.java
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
**Error:** `class helloworld is public, should be declared in a file named helloworld.java`

✅ **Correct:**
```java
public class HelloWorld {  // Filename: HelloWorld.java
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### 2. Missing Semicolon

❌ **Wrong:**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!")  // Missing semicolon
    }
}
```
**Error:** `';' expected`

✅ **Correct:**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");  // Semicolon added
    }
}
```

### 3. Incorrect main Method Signature

❌ **Wrong:**
```java
public class HelloWorld {
    public void main(String[] args) {  // Missing 'static'
        System.out.println("Hello, World!");
    }
}
```
**Error:** `Main method not found`

✅ **Correct:**
```java
public class HelloWorld {
    public static void main(String[] args) {  // 'static' keyword added
        System.out.println("Hello, World!");
    }
}
```

### 4. Case Sensitivity Issues

❌ **Wrong:**
```java
public class HelloWorld {
    public static void main(String[] args) {
        system.out.println("Hello, World!");  // 'system' should be 'System'
    }
}
```
**Error:** `cannot find symbol: variable system`

✅ **Correct:**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");  // 'System' with capital S
    }
}
```

## Understanding the Compilation Process

```
Source Code (.java) → Compiler (javac) → Bytecode (.class) → JVM → Output
```

### What Happens When You Compile?

1. **Syntax Check**: Compiler checks for syntax errors
2. **Type Checking**: Verifies data types are used correctly
3. **Bytecode Generation**: Creates platform-independent bytecode
4. **Class File Creation**: Saves bytecode in `.class` file

### What Happens When You Run?

1. **Class Loading**: JVM loads the `.class` file
2. **Bytecode Verification**: Ensures bytecode is valid and secure
3. **JIT Compilation**: Converts bytecode to native machine code
4. **Execution**: Runs the program starting from `main` method

## Extended Examples

### 1. Hello World with User Input

```java
import java.util.Scanner;

public class HelloWorld {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        
        System.out.println("Hello, " + name + "!");
        scanner.close();
    }
}
```

### 2. Hello World with Command Line Arguments

```java
public class HelloWorld {
    public static void main(String[] args) {
        if (args.length > 0) {
            System.out.println("Hello, " + args[0] + "!");
        } else {
            System.out.println("Hello, World!");
        }
    }
}
```

Run with:
```bash
java HelloWorld Alice
```
Output:
```
Hello, Alice!
```

### 3. Hello World with Current Date and Time

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class HelloWorld {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        
        System.out.println("Hello, World!");
        System.out.println("Current date and time: " + now.format(formatter));
    }
}
```

## Java Program Structure Rules

### 1. Package Declaration (Optional)
```java
package com.example;  // Must be first line if present
```

### 2. Import Statements (Optional)
```java
import java.util.Scanner;  // After package, before class
```

### 3. Class Declaration (Required)
```java
public class HelloWorld {  // One public class per file
    // Class members
}
```

### 4. Class Members
- Variables (fields)
- Methods
- Constructors
- Nested classes

### 5. Method Structure
```java
access_modifier return_type method_name(parameters) {
    // method body
}
```

## Best Practices

1. **Naming Conventions**:
   - Classes: PascalCase (e.g., `HelloWorld`)
   - Methods: camelCase (e.g., `printMessage`)
   - Constants: UPPER_SNAKE_CASE (e.g., `MAX_VALUE`)
   - Variables: camelCase (e.g., `userName`)

2. **Indentation**: Use consistent indentation (typically 4 spaces)

3. **Comments**: Add meaningful comments to explain complex logic

4. **File Organization**: One public class per file

5. **Code Formatting**: Keep lines under 80-120 characters

## Practice Exercises

1. **Exercise 1**: Modify the Hello World program to print your name and age.

2. **Exercise 2**: Create a program that prints a simple ASCII art.

3. **Exercise 3**: Write a program that prints "Hello, World!" in 5 different languages.

4. **Exercise 4**: Create a program that prints a multiplication table of 5.

5. **Exercise 5**: Write a program that prints the following pattern:
   ```
   *
   **
   ***
   ****
   *****
   ```

## Summary

The Hello World program teaches us:
- Basic Java program structure
- The importance of the `main` method
- How to output text using `System.out.println()`
- Java syntax rules and case sensitivity
- The compilation and execution process

This simple program forms the foundation for all Java applications. Every Java developer, regardless of experience level, started with this exact program!

## Next Steps

Now that you understand the basic structure of a Java program:
1. Learn about variables and data types
2. Explore different operators in Java
3. Understand control flow statements
4. Practice writing more complex programs

---

*Remember: Every expert was once a beginner. Your journey in Java programming has just begun!*