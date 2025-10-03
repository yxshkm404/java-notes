# String in Java - Introduction

## What is a String?

A String in Java is a sequence of characters used to represent text. Unlike primitive data types, String is a reference type (object) that belongs to the `java.lang` package. Strings are one of the most frequently used classes in Java programming and have special treatment in the language.

![Java String](https://raw.githubusercontent.com/github/explore/5b3600551e122a3277c2c5368af2ad5725ffa9a1/topics/java/java.png)

## Key Characteristics of Strings

### 1. Strings are Immutable

Once a String object is created, it cannot be changed. Any operation that appears to modify a String actually creates a new String object.

```java
public class StringImmutability {
    public static void main(String[] args) {
        String str = "Hello";
        str.concat(" World");  // Creates new String, doesn't modify original
        System.out.println(str);  // Still prints "Hello"
        
        // To see the change, assign it back
        str = str.concat(" World");
        System.out.println(str);  // Now prints "Hello World"
    }
}
```

### 2. String is a Class, Not a Primitive Type

```java
public class StringAsObject {
    public static void main(String[] args) {
        // String is an object
        String name = new String("Java");  // Using constructor
        String language = "Java";          // Using string literal
        
        // Can call methods on String objects
        int length = name.length();
        char firstChar = name.charAt(0);
        
        System.out.println("Length: " + length);
        System.out.println("First character: " + firstChar);
    }
}
```

### 3. Special Support in Java

Despite being an object, String has special support in Java:
- String literals
- String concatenation with `+` operator  
- Automatic conversion in print statements

## Creating Strings

### Method 1: Using String Literals

The most common and memory-efficient way to create strings.

```java
public class StringLiterals {
    public static void main(String[] args) {
        String str1 = "Hello World";
        String str2 = "Java Programming";
        String empty = "";  // Empty string
        
        // String literals are stored in String Pool
        String str3 = "Hello World";
        
        // str1 and str3 refer to same object in String Pool
        System.out.println(str1 == str3);  // true
    }
}
```

### Method 2: Using String Constructor

Creates a new String object in heap memory.

```java
public class StringConstructor {
    public static void main(String[] args) {
        // Different String constructors
        String str1 = new String();  // Empty string
        String str2 = new String("Hello");
        
        // From character array
        char[] chars = {'J', 'a', 'v', 'a'};
        String str3 = new String(chars);
        
        // From byte array
        byte[] bytes = {72, 101, 108, 108, 111};  // ASCII values
        String str4 = new String(bytes);
        
        // From StringBuffer/StringBuilder
        StringBuffer buffer = new StringBuffer("Hello");
        String str5 = new String(buffer);
        
        System.out.println("From chars: " + str3);
        System.out.println("From bytes: " + str4);
    }
}
```

## String Pool (String Constant Pool)

Java maintains a special memory area called String Pool to optimize memory usage for strings.

```java
public class StringPoolDemo {
    public static void main(String[] args) {
        // String literals go to String Pool
        String str1 = "Hello";
        String str2 = "Hello";
        
        // Same reference (from pool)
        System.out.println("str1 == str2: " + (str1 == str2));  // true
        
        // Using new creates object in heap
        String str3 = new String("Hello");
        
        // Different reference (heap vs pool)
        System.out.println("str1 == str3: " + (str1 == str3));  // false
        
        // But same content
        System.out.println("str1.equals(str3): " + str1.equals(str3));  // true
        
        // intern() method adds string to pool
        String str4 = str3.intern();
        System.out.println("str1 == str4: " + (str1 == str4));  // true
    }
}
```

### String Pool Visualization

```
String Pool (Method Area/Heap)
┌─────────────────────────┐
│   "Hello"    ←─ str1    │
│      ↑          str2    │
│      └─────────→str4    │
│   "World"               │
│   "Java"                │
└─────────────────────────┘

Heap Memory
┌─────────────────────────┐
│   new String("Hello")   │ ← str3
│                         │
└─────────────────────────┘
```

## String Concatenation

### Using + Operator

```java
public class StringConcatenation {
    public static void main(String[] args) {
        String firstName = "John";
        String lastName = "Doe";
        
        // Using + operator
        String fullName = firstName + " " + lastName;
        System.out.println(fullName);  // John Doe
        
        // Concatenating with other types
        int age = 25;
        String info = "Name: " + fullName + ", Age: " + age;
        System.out.println(info);
        
        // Order matters with numbers
        System.out.println("Sum: " + 10 + 20);     // Sum: 1020
        System.out.println("Sum: " + (10 + 20));   // Sum: 30
        System.out.println(10 + 20 + " is sum");   // 30 is sum
    }
}
```

### Using concat() Method

```java
public class ConcatMethod {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = " World";
        
        String result = str1.concat(str2);
        System.out.println(result);  // Hello World
        
        // Chaining concat
        String message = "Java".concat(" is").concat(" awesome!");
        System.out.println(message);
        
        // concat only works with strings
        // str1.concat(123);  // Compilation error
        str1 = str1.concat(String.valueOf(123));  // Convert to String first
    }
}
```

## Basic String Operations

### 1. Length and Character Access

```java
public class StringBasicOps {
    public static void main(String[] args) {
        String text = "Java Programming";
        
        // Length of string
        System.out.println("Length: " + text.length());  // 16
        
        // Access individual characters
        System.out.println("First char: " + text.charAt(0));      // 'J'
        System.out.println("Last char: " + text.charAt(text.length() - 1));  // 'g'
        
        // Get substring
        System.out.println("Substring(0,4): " + text.substring(0, 4));  // "Java"
        System.out.println("Substring(5): " + text.substring(5));       // "Programming"
        
        // IndexOf
        System.out.println("Index of 'a': " + text.indexOf('a'));      // 1
        System.out.println("Last index of 'a': " + text.lastIndexOf('a'));  // 10
    }
}
```

### 2. String Comparison

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = new String("Hello");
        String str4 = "hello";
        
        // Using == (compares references)
        System.out.println("str1 == str2: " + (str1 == str2));     // true
        System.out.println("str1 == str3: " + (str1 == str3));     // false
        
        // Using equals() (compares content)
        System.out.println("str1.equals(str2): " + str1.equals(str2));  // true
        System.out.println("str1.equals(str3): " + str1.equals(str3));  // true
        System.out.println("str1.equals(str4): " + str1.equals(str4));  // false
        
        // Case-insensitive comparison
        System.out.println("str1.equalsIgnoreCase(str4): " + 
                          str1.equalsIgnoreCase(str4));  // true
        
        // compareTo() for alphabetical ordering
        System.out.println("str1.compareTo(str4): " + str1.compareTo(str4));  // negative
    }
}
```

### 3. String Case Conversion

```java
public class StringCaseConversion {
    public static void main(String[] args) {
        String text = "Java Programming Language";
        
        // Convert to uppercase
        String upper = text.toUpperCase();
        System.out.println("Uppercase: " + upper);  // JAVA PROGRAMMING LANGUAGE
        
        // Convert to lowercase
        String lower = text.toLowerCase();
        System.out.println("Lowercase: " + lower);  // java programming language
        
        // Original string unchanged
        System.out.println("Original: " + text);    // Java Programming Language
        
        // Practical example
        String userInput = "YES";
        if (userInput.toLowerCase().equals("yes")) {
            System.out.println("User agreed!");
        }
    }
}
```

### 4. String Trimming and Checking

```java
public class StringTrimCheck {
    public static void main(String[] args) {
        String text = "  Java Programming  ";
        
        // Remove leading and trailing whitespace
        String trimmed = text.trim();
        System.out.println("Original: '" + text + "'");
        System.out.println("Trimmed: '" + trimmed + "'");
        
        // Check if string is empty
        String empty = "";
        String blank = "   ";
        
        System.out.println("empty.isEmpty(): " + empty.isEmpty());        // true
        System.out.println("blank.isEmpty(): " + blank.isEmpty());        // false
        System.out.println("blank.trim().isEmpty(): " + blank.trim().isEmpty());  // true
        
        // Java 11+ has isBlank()
        // System.out.println("blank.isBlank(): " + blank.isBlank());     // true
        
        // Check start and end
        String filename = "document.pdf";
        System.out.println("Starts with 'doc': " + filename.startsWith("doc"));  // true
        System.out.println("Ends with '.pdf': " + filename.endsWith(".pdf"));    // true
    }
}
```

## Escape Sequences in Strings

```java
public class EscapeSequences {
    public static void main(String[] args) {
        // Common escape sequences
        System.out.println("Hello\nWorld");          // New line
        System.out.println("Hello\tWorld");          // Tab
        System.out.println("Hello \"World\"");       // Double quotes
        System.out.println("Hello \'World\'");       // Single quotes
        System.out.println("Hello\\World");          // Backslash
        System.out.println("Hello\rWorld");          // Carriage return
        System.out.println("Hello\bWorld");          // Backspace
        System.out.println("Hello\fWorld");          // Form feed
        
        // File paths
        String windowsPath = "C:\\Users\\Documents\\file.txt";
        System.out.println("Windows path: " + windowsPath);
        
        // Unicode characters
        String unicode = "Java \u2764 Programming";  // Heart symbol
        System.out.println(unicode);
    }
}
```

## Common String Operations Examples

### Example 1: Extracting Information

```java
public class StringExtraction {
    public static void main(String[] args) {
        String email = "john.doe@example.com";
        
        // Extract username
        int atIndex = email.indexOf('@');
        String username = email.substring(0, atIndex);
        System.out.println("Username: " + username);  // john.doe
        
        // Extract domain
        String domain = email.substring(atIndex + 1);
        System.out.println("Domain: " + domain);      // example.com
        
        // Extract file extension
        String filename = "document.pdf";
        int dotIndex = filename.lastIndexOf('.');
        String extension = filename.substring(dotIndex + 1);
        System.out.println("Extension: " + extension);  // pdf
    }
}
```

### Example 2: String Validation

```java
public class StringValidation {
    public static void main(String[] args) {
        // Validate email format (simple)
        String email = "user@example.com";
        boolean isValidEmail = email.contains("@") && 
                               email.indexOf("@") < email.lastIndexOf(".");
        System.out.println("Valid email? " + isValidEmail);
        
        // Check if string contains only digits
        String number = "12345";
        boolean isNumeric = true;
        for (int i = 0; i < number.length(); i++) {
            if (!Character.isDigit(number.charAt(i))) {
                isNumeric = false;
                break;
            }
        }
        System.out.println("Is numeric? " + isNumeric);
        
        // Check if string is palindrome
        String word = "radar";
        String reversed = new StringBuilder(word).reverse().toString();
        boolean isPalindrome = word.equals(reversed);
        System.out.println(word + " is palindrome? " + isPalindrome);
    }
}
```

### Example 3: String Formatting

```java
public class StringFormatting {
    public static void main(String[] args) {
        // Using String.format()
        String name = "John";
        int age = 25;
        double salary = 50000.50;
        
        String formatted = String.format("Name: %s, Age: %d, Salary: $%.2f", 
                                       name, age, salary);
        System.out.println(formatted);
        
        // Padding and alignment
        System.out.println(String.format("|%-10s|%10s|", "Left", "Right"));
        System.out.println(String.format("|%-10d|%10d|", 123, 456));
        
        // Date formatting
        String date = String.format("Today is %tB %<te, %<tY", 
                                   new java.util.Date());
        System.out.println(date);
    }
}
```

## String vs char[]

```java
public class StringVsCharArray {
    public static void main(String[] args) {
        // String to char array
        String str = "Hello";
        char[] chars = str.toCharArray();
        
        // Modify char array
        chars[0] = 'J';
        System.out.println("Modified array: " + new String(chars));  // Jello
        System.out.println("Original string: " + str);               // Hello
        
        // char array to String
        char[] vowels = {'a', 'e', 'i', 'o', 'u'};
        String vowelString = new String(vowels);
        System.out.println("Vowels: " + vowelString);
        
        // Why use char[] for passwords?
        // char[] can be modified and cleared from memory
        char[] password = {'s', 'e', 'c', 'r', 'e', 't'};
        // Use password...
        // Clear sensitive data
        java.util.Arrays.fill(password, ' ');
    }
}
```

## String Performance Considerations

```java
public class StringPerformance {
    public static void main(String[] args) {
        // Inefficient string concatenation in loop
        String result = "";
        long startTime = System.currentTimeMillis();
        
        for (int i = 0; i < 1000; i++) {
            result += "a";  // Creates new String object each time
        }
        
        long endTime = System.currentTimeMillis();
        System.out.println("String concat time: " + (endTime - startTime) + "ms");
        
        // Efficient using StringBuilder
        StringBuilder sb = new StringBuilder();
        startTime = System.currentTimeMillis();
        
        for (int i = 0; i < 1000; i++) {
            sb.append("a");
        }
        result = sb.toString();
        
        endTime = System.currentTimeMillis();
        System.out.println("StringBuilder time: " + (endTime - startTime) + "ms");
    }
}
```

## Common String Mistakes and Solutions

### Mistake 1: Using == for String Comparison

```java
public class StringMistakes {
    public static void main(String[] args) {
        // Wrong way
        String input = new String("yes");
        if (input == "yes") {  // Wrong! Compares references
            System.out.println("This might not work!");
        }
        
        // Correct way
        if (input.equals("yes")) {  // Correct! Compares content
            System.out.println("This works!");
        }
        
        // Safe null handling
        String maybeNull = null;
        // if (maybeNull.equals("test")) {}  // NullPointerException!
        
        if ("test".equals(maybeNull)) {  // Safe - no NPE
            System.out.println("Equal");
        }
    }
}
```

### Mistake 2: Forgetting String Immutability

```java
public class ImmutabilityMistake {
    public static void main(String[] args) {
        String name = "John";
        name.toUpperCase();  // This doesn't change 'name'
        System.out.println(name);  // Still prints "John"
        
        // Correct way
        name = name.toUpperCase();  // Assign back
        System.out.println(name);    // Now prints "JOHN"
        
        // Method that seems to modify string
        modifyString(name);
        System.out.println(name);    // Still "JOHN" - not modified
    }
    
    static void modifyString(String str) {
        str = "Modified";  // Only changes local reference
    }
}
```

## Memory Representation

```java
public class StringMemory {
    public static void main(String[] args) {
        // Memory allocation visualization
        String s1 = "Java";      // String Pool
        String s2 = "Java";      // Reuses from Pool
        String s3 = new String("Java");  // Heap
        String s4 = s3.intern(); // Returns Pool reference
        
        System.out.println("s1 == s2: " + (s1 == s2));  // true (same pool object)
        System.out.println("s1 == s3: " + (s1 == s3));  // false (pool vs heap)
        System.out.println("s1 == s4: " + (s1 == s4));  // true (both pool)
        
        // Memory diagram
        /*
         * String Pool:
         * ┌──────────┐
         * │  "Java"  │ ← s1, s2, s4
         * └──────────┘
         * 
         * Heap:
         * ┌──────────┐
         * │  "Java"  │ ← s3
         * └──────────┘
         */
    }
}
```

## Practice Exercises

1. **Reverse a String**: Write a method to reverse a string without using StringBuilder
2. **Count Vowels**: Count the number of vowels in a given string
3. **Remove Duplicates**: Remove duplicate characters from a string
4. **Check Anagram**: Check if two strings are anagrams
5. **Title Case**: Convert a sentence to title case (first letter of each word capitalized)

## Summary

Key points about Strings in Java:

1. **Immutable**: Strings cannot be changed after creation
2. **Object Type**: String is a reference type, not primitive
3. **String Pool**: Literals are stored in a special memory area
4. **Special Support**: Has operator overloading (+) and literals
5. **Rich API**: Provides many useful methods for manipulation
6. **Performance**: Use StringBuilder/StringBuffer for multiple concatenations

## Next Topics

- StringBuilder and StringBuffer
- Regular Expressions with Strings
- String formatting and parsing
- Internationalization with Strings
- String algorithms and patterns

---

*Strings are fundamental to Java programming. Master these concepts to handle text effectively in your applications!*