# Data Types & Ranges in Java

## Introduction

Data types in Java specify the size and type of values that can be stored in variables. Java is a statically-typed language, which means you must declare the data type of a variable before using it. Understanding data types and their ranges is crucial for efficient memory usage and preventing data overflow errors.

![Java Data Types](https://scaler.com/topics/images/java-data-types.webp)

## Categories of Data Types

Java data types are broadly classified into two categories:

1. **Primitive Data Types** (Built-in types)
2. **Non-Primitive Data Types** (Reference types)

## Primitive Data Types

Java has 8 primitive data types that are predefined by the language and named by reserved keywords.

![Data Type Ranges](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRtST7I0WolMsjHuOu5UgWP-a785OyKl8ylVw&s)

### 1. byte

The smallest integer data type, useful for saving memory in large arrays.

```java
public class ByteExample {
    public static void main(String[] args) {
        byte minByte = -128;
        byte maxByte = 127;
        byte defaultByte = 0;
        
        System.out.println("byte range: " + minByte + " to " + maxByte);
        System.out.println("byte size: " + Byte.SIZE + " bits");
        System.out.println("byte bytes: " + Byte.BYTES + " byte");
        
        // byte overflow example
        // byte overflow = 128;  // Error: incompatible types
    }
}
```

**Characteristics:**
- Size: 8 bits (1 byte)
- Range: -128 to 127 (-2^7 to 2^7 - 1)
- Default value: 0
- Use case: Saving memory in large arrays

### 2. short

A 16-bit signed integer, rarely used in modern programming.

```java
public class ShortExample {
    public static void main(String[] args) {
        short minShort = -32768;
        short maxShort = 32767;
        short temperature = -10;
        short year = 2024;
        
        System.out.println("short range: " + Short.MIN_VALUE + " to " + Short.MAX_VALUE);
        System.out.println("short size: " + Short.SIZE + " bits");
        
        // Type casting required for arithmetic
        short a = 10;
        short b = 20;
        // short c = a + b;  // Error: requires casting
        short c = (short)(a + b);  // Correct
    }
}
```

**Characteristics:**
- Size: 16 bits (2 bytes)
- Range: -32,768 to 32,767 (-2^15 to 2^15 - 1)
- Default value: 0
- Use case: When memory is at premium and value range is known

### 3. int

The most commonly used integer type in Java.

```java
public class IntExample {
    public static void main(String[] args) {
        int minInt = Integer.MIN_VALUE;  // -2,147,483,648
        int maxInt = Integer.MAX_VALUE;  // 2,147,483,647
        
        // Different ways to declare integers
        int decimal = 100;           // Decimal
        int binary = 0b1100100;      // Binary (prefix 0b)
        int octal = 0144;            // Octal (prefix 0)
        int hexadecimal = 0x64;      // Hexadecimal (prefix 0x)
        
        // Underscore in numeric literals (Java 7+)
        int million = 1_000_000;
        int creditCard = 1234_5678_9012_3456;
        
        System.out.println("All represent same value: " + decimal);
        System.out.println("Million: " + million);
        
        // Integer overflow
        System.out.println("Max int + 1 = " + (maxInt + 1));  // Wraps to negative
    }
}
```

**Characteristics:**
- Size: 32 bits (4 bytes)
- Range: -2,147,483,648 to 2,147,483,647 (-2^31 to 2^31 - 1)
- Default value: 0
- Use case: Default choice for integer values

### 4. long

Used for larger integer values that exceed int range.

```java
public class LongExample {
    public static void main(String[] args) {
        long minLong = Long.MIN_VALUE;
        long maxLong = Long.MAX_VALUE;
        
        // Long literals require 'L' suffix
        long bigNumber = 9223372036854775807L;
        long population = 8_000_000_000L;  // World population
        
        // Time calculations
        long milliseconds = System.currentTimeMillis();
        long nanoseconds = System.nanoTime();
        
        System.out.println("long range: " + minLong + " to " + maxLong);
        System.out.println("Current time in ms: " + milliseconds);
        
        // Conversion from int
        int intValue = 100;
        long longValue = intValue;  // Automatic widening
    }
}
```

**Characteristics:**
- Size: 64 bits (8 bytes)
- Range: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (-2^63 to 2^63 - 1)
- Default value: 0L
- Use case: Large numbers, timestamps, file sizes

### 5. float

Single-precision floating-point number.

```java
public class FloatExample {
    public static void main(String[] args) {
        // Float literals require 'f' suffix
        float pi = 3.14159f;
        float temperature = -40.5f;
        float scientific = 6.022e23f;  // Scientific notation
        
        System.out.println("float range: " + Float.MIN_VALUE + " to " + Float.MAX_VALUE);
        System.out.println("float precision: ~7 decimal digits");
        
        // Special float values
        float positiveInfinity = Float.POSITIVE_INFINITY;
        float negativeInfinity = Float.NEGATIVE_INFINITY;
        float notANumber = Float.NaN;
        
        // Precision limitation
        float precise = 1.123456789f;
        System.out.println("Precision loss: " + precise);  // Shows ~7 digits
        
        // Float arithmetic
        float result = 0.1f + 0.2f;
        System.out.println("0.1f + 0.2f = " + result);  // May not be exactly 0.3
    }
}
```

**Characteristics:**
- Size: 32 bits (4 bytes)
- Range: ~±1.4E-45 to ±3.4E+38
- Precision: ~6-7 significant decimal digits
- Default value: 0.0f
- Use case: Scientific calculations where memory is limited

### 6. double

Double-precision floating-point number (default for decimals).

```java
public class DoubleExample {
    public static void main(String[] args) {
        // Double is default for decimal numbers
        double pi = 3.141592653589793;
        double avogadro = 6.022140857e23;
        double planck = 6.62607015e-34;
        
        System.out.println("double range: " + Double.MIN_VALUE + " to " + Double.MAX_VALUE);
        System.out.println("double precision: ~15-16 decimal digits");
        
        // Special double values
        double infinity = Double.POSITIVE_INFINITY;
        double nan = Double.NaN;
        
        // Precision comparison
        double preciseValue = 1.123456789012345678;
        System.out.println("Double precision: " + preciseValue);
        
        // Mathematical operations
        double sqrt = Math.sqrt(2.0);
        double power = Math.pow(2.0, 10.0);
        
        // Currency calculations (not recommended)
        double price = 19.99;
        double tax = 0.08;
        double total = price * (1 + tax);  // May have precision issues
    }
}
```

**Characteristics:**
- Size: 64 bits (8 bytes)
- Range: ~±4.9E-324 to ±1.8E+308
- Precision: ~15-16 significant decimal digits
- Default value: 0.0d
- Use case: Default for decimal values, scientific calculations

### 7. char

Represents a single Unicode character.

```java
public class CharExample {
    public static void main(String[] args) {
        // Different ways to declare char
        char letter = 'A';
        char digit = '5';
        char unicode = '\u0041';      // Unicode for 'A'
        char escape = '\n';           // Newline character
        char emoji = '😊';            // Unicode emoji (requires proper encoding)
        
        System.out.println("char size: " + Character.SIZE + " bits");
        System.out.println("char range: " + (int)Character.MIN_VALUE + 
                          " to " + (int)Character.MAX_VALUE);
        
        // Char as numeric value
        char ch = 65;  // ASCII/Unicode value for 'A'
        System.out.println("Char 65: " + ch);
        
        // Character operations
        char lowercase = 'a';
        char uppercase = Character.toUpperCase(lowercase);
        System.out.println(lowercase + " -> " + uppercase);
        
        // Escape sequences
        System.out.println("Tab:\tspace");
        System.out.println("Quote: \"Hello\"");
        System.out.println("Backslash: \\");
    }
}
```

**Characteristics:**
- Size: 16 bits (2 bytes)
- Range: 0 to 65,535 (Unicode characters)
- Default value: '\u0000' (null character)
- Use case: Storing single characters, text processing

### 8. boolean

Represents true or false values.

```java
public class BooleanExample {
    public static void main(String[] args) {
        boolean isJavaFun = true;
        boolean isComplete = false;
        
        // Boolean from expressions
        boolean isAdult = 25 > 18;
        boolean isEqual = (10 == 10);
        boolean isValid = (5 > 3) && (10 < 20);
        
        System.out.println("isJavaFun: " + isJavaFun);
        System.out.println("isAdult: " + isAdult);
        
        // Boolean in conditions
        if (isValid) {
            System.out.println("Condition is valid");
        }
        
        // Boolean operations
        boolean and = true && false;    // false
        boolean or = true || false;     // true
        boolean not = !true;            // false
        boolean xor = true ^ false;     // true
        
        // Note: boolean size is JVM-dependent (typically 1 bit, but may use 1 byte)
    }
}
```

**Characteristics:**
- Size: JVM dependent (typically 1 bit, stored as 1 byte)
- Values: true or false only
- Default value: false
- Use case: Conditional logic, flags

## Type Conversion and Casting

### Widening (Automatic) Conversion

Conversion from smaller to larger type happens automatically.

```java
public class WideningExample {
    public static void main(String[] args) {
        // Widening conversion hierarchy
        // byte -> short -> int -> long -> float -> double
        
        byte byteValue = 10;
        short shortValue = byteValue;    // byte to short
        int intValue = shortValue;        // short to int
        long longValue = intValue;        // int to long
        float floatValue = longValue;     // long to float
        double doubleValue = floatValue;  // float to double
        
        System.out.println("Original byte: " + byteValue);
        System.out.println("Final double: " + doubleValue);
        
        // char can be widened to int
        char ch = 'A';
        int charValue = ch;  // 65
        System.out.println("Char 'A' as int: " + charValue);
    }
}
```

### Narrowing (Explicit) Conversion

Conversion from larger to smaller type requires explicit casting.

```java
public class NarrowingExample {
    public static void main(String[] args) {
        // Narrowing requires explicit cast
        double doubleValue = 100.99;
        float floatValue = (float) doubleValue;
        long longValue = (long) floatValue;
        int intValue = (int) longValue;
        short shortValue = (short) intValue;
        byte byteValue = (byte) shortValue;
        
        System.out.println("Original double: " + doubleValue);
        System.out.println("Final byte: " + byteValue);  // Loss of decimal
        
        // Overflow example
        int bigInt = 300;
        byte smallByte = (byte) bigInt;  // Overflow!
        System.out.println("300 as byte: " + smallByte);  // Result: 44
        
        // Safe casting with bounds checking
        if (bigInt >= Byte.MIN_VALUE && bigInt <= Byte.MAX_VALUE) {
            byte safeByte = (byte) bigInt;
        } else {
            System.out.println("Value out of byte range!");
        }
    }
}
```

## Non-Primitive (Reference) Data Types

### String

Though String is a reference type, it's used so commonly that it feels like a primitive.

```java
public class StringExample {
    public static void main(String[] args) {
        // String declaration
        String name = "Java";
        String empty = "";
        String nullString = null;
        
        // String is immutable
        String original = "Hello";
        String modified = original + " World";  // Creates new String
        
        System.out.println("Original unchanged: " + original);
        System.out.println("New string: " + modified);
        
        // String methods
        String text = "  Java Programming  ";
        System.out.println("Length: " + text.length());
        System.out.println("Trimmed: " + text.trim());
        System.out.println("Uppercase: " + text.toUpperCase());
        System.out.println("Contains 'Java': " + text.contains("Java"));
    }
}
```

### Arrays

Arrays are reference types that hold multiple values of the same type.

```java
public class ArrayExample {
    public static void main(String[] args) {
        // Array declarations
        int[] numbers = new int[5];           // Array of 5 integers
        double[] prices = {19.99, 29.99, 39.99};  // Array initialization
        String[] names = new String[3];       // Array of strings
        
        // Accessing and modifying arrays
        numbers[0] = 10;
        numbers[1] = 20;
        
        System.out.println("First number: " + numbers[0]);
        System.out.println("Array length: " + numbers.length);
        
        // Multi-dimensional arrays
        int[][] matrix = new int[3][3];
        int[][] predefined = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    }
}
```

### Classes and Objects

User-defined reference types.

```java
public class ClassExample {
    public static void main(String[] args) {
        // Creating objects
        Person person = new Person("John", 25);
        Date today = new Date();
        ArrayList<Integer> list = new ArrayList<>();
        
        // Reference behavior
        Person person1 = new Person("Alice", 30);
        Person person2 = person1;  // Both refer to same object
        person2.setName("Bob");
        System.out.println(person1.getName());  // Prints "Bob"
    }
}

class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Getters and setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```

## Memory Size and Performance Comparison

```java
public class MemoryComparison {
    public static void main(String[] args) {
        System.out.println("=== Primitive Type Sizes ===");
        System.out.println("boolean: ~1 bit (1 byte in practice)");
        System.out.println("byte:    " + Byte.BYTES + " byte");
        System.out.println("short:   " + Short.BYTES + " bytes");
        System.out.println("char:    " + Character.BYTES + " bytes");
        System.out.println("int:     " + Integer.BYTES + " bytes");
        System.out.println("float:   " + Float.BYTES + " bytes");
        System.out.println("long:    " + Long.BYTES + " bytes");
        System.out.println("double:  " + Double.BYTES + " bytes");
        
        System.out.println("\n=== Memory Usage Example ===");
        // Array of 1 million integers
        int[] intArray = new int[1_000_000];
        long intMemory = (long) Integer.BYTES * 1_000_000;
        System.out.println("1M integers: " + intMemory / (1024 * 1024) + " MB");
        
        // Same data as byte array (if values fit)
        byte[] byteArray = new byte[1_000_000];
        long byteMemory = (long) Byte.BYTES * 1_000_000;
        System.out.println("1M bytes: " + byteMemory / (1024 * 1024) + " MB");
    }
}
```

## Wrapper Classes

Each primitive type has a corresponding wrapper class.

```java
public class WrapperClassExample {
    public static void main(String[] args) {
        // Wrapper classes for primitives
        Boolean boolObj = true;
        Byte byteObj = 127;
        Short shortObj = 32767;
        Character charObj = 'A';
        Integer intObj = 2147483647;
        Float floatObj = 3.14f;
        Long longObj = 9223372036854775807L;
        Double doubleObj = 3.141592653589793;
        
        // Autoboxing (primitive to wrapper)
        Integer autoBoxed = 100;  // int to Integer
        
        // Unboxing (wrapper to primitive)
        int unboxed = autoBoxed;  // Integer to int
        
        // Useful wrapper class methods
        int parsed = Integer.parseInt("123");
        String binary = Integer.toBinaryString(42);
        String hex = Integer.toHexString(255);
        
        System.out.println("Parsed: " + parsed);
        System.out.println("42 in binary: " + binary);
        System.out.println("255 in hex: " + hex);
        
        // Null handling with wrappers
        Integer nullable = null;
        // int primitive = nullable;  // NullPointerException!
    }
}
```

## Choosing the Right Data Type

### Guidelines for Selection

```java
public class DataTypeSelection {
    public static void main(String[] args) {
        // For whole numbers
        byte age = 25;                    // Age unlikely to exceed 127
        short year = 2024;                // Year fits in short range
        int population = 1_400_000_000;   // City/country population
        long worldPopulation = 8_000_000_000L;  // World population
        
        // For decimals
        float temperature = 98.6f;        // Weather/body temperature
        double scientificValue = 6.022e23; // Scientific calculations
        
        // For text
        char grade = 'A';                 // Single character
        String name = "Java Developer";   // Text/strings
        
        // For logic
        boolean isActive = true;          // True/false flags
        
        // For money (use BigDecimal, not float/double)
        // BigDecimal price = new BigDecimal("19.99");
    }
}
```

## Common Pitfalls and Best Practices

### 1. Integer Overflow

```java
public class OverflowExample {
    public static void main(String[] args) {
        int maxInt = Integer.MAX_VALUE;
        System.out.println("Max int: " + maxInt);
        System.out.println("Max int + 1: " + (maxInt + 1));  // Overflow!
        
        // Safe addition with overflow check
        try {
            int result = Math.addExact(maxInt, 1);
        } catch (ArithmeticException e) {
            System.out.println("Overflow detected!");
        }
    }
}
```

### 2. Floating-Point Precision

```java
public class FloatingPointPitfalls {
    public static void main(String[] args) {
        // Precision issues
        double result = 0.1 + 0.2;
        System.out.println("0.1 + 0.2 = " + result);  // Not exactly 0.3!
        System.out.println("Is 0.3? " + (result == 0.3));  // false!
        
        // Comparing floating-point numbers
        double EPSILON = 0.0000001;
        boolean isEqual = Math.abs(result - 0.3) < EPSILON;
        System.out.println("Approximately equal? " + isEqual);  // true
        
        // For money, use BigDecimal
        // BigDecimal price1 = new BigDecimal("0.1");
        // BigDecimal price2 = new BigDecimal("0.2");
        // BigDecimal total = price1.add(price2);  // Exactly 0.3
    }
}
```

### 3. Character Encoding

```java
public class CharacterEncoding {
    public static void main(String[] args) {
        // ASCII characters
        char asciiA = 'A';
        char ascii65 = 65;
        System.out.println("Both are 'A': " + asciiA + " and " + ascii65);
        
        // Unicode characters
        char copyright = '\u00A9';
        char euro = '\u20AC';
        System.out.println("Copyright: " + copyright);
        System.out.println("Euro: " + euro);
        
        // Character arithmetic
        char nextChar = (char) (asciiA + 1);  // 'B'
        System.out.println("Next char after A: " + nextChar);
    }
}
```

## Practice Examples

### Example 1: Data Type Range Validator

```java
public class RangeValidator {
    public static void main(String[] args) {
        // Check if a value fits in different types
        long testValue = 1000;
        
        System.out.println("Value: " + testValue);
        System.out.println("Fits in byte? " + 
            (testValue >= Byte.MIN_VALUE && testValue <= Byte.MAX_VALUE));
        System.out.println("Fits in short? " + 
            (testValue >= Short.MIN_VALUE && testValue <= Short.MAX_VALUE));
        System.out.println("Fits in int? " + 
            (testValue >= Integer.MIN_VALUE && testValue <= Integer.MAX_VALUE));
    }
}
```

### Example 2: Type Size Calculator

```java
public class TypeSizeCalculator {
    public static void main(String[] args) {
        // Calculate memory for different array sizes
        int elements = 1_000_000;
        
        System.out.println("Memory required for " + elements + " elements:");
        System.out.println("byte[]:   " + (elements * Byte.BYTES / 1024) + " KB");
        System.out.println("short[]:  " + (elements * Short.BYTES / 1024) + " KB");
        System.out.println("int[]:    " + (elements * Integer.BYTES / 1024) + " KB");
        System.out.println("long[]:   " + (elements * Long.BYTES / 1024) + " KB");
        System.out.println("float[]:  " + (elements * Float.BYTES / 1024) + " KB");
        System.out.println("double[]: " + (elements * Double.BYTES / 1024) + " KB");
    }
}
```

## Summary

Understanding data types and their ranges is fundamental to Java programming:

1. **Choose appropriately**: Select the smallest type that can hold your data
2. **Watch for overflow**: Be aware of type limits to prevent overflow
3. **Precision matters**: Understand floating-point limitations
4. **Memory efficiency**: Smaller types save memory in large arrays
5. **Type safety**: Java's strong typing helps prevent errors

## Quick Reference Table

| Type    | Size    | Range                           | Default | Wrapper   |
|---------|---------|--------------------------------|---------|-----------|
| boolean | ~1 bit  | true/false                     | false   | Boolean   |
| byte    | 8 bits  | -128 to 127                    | 0       | Byte      |
| short   | 16 bits | -32,768 to 32,767             | 0       | Short     |
| char    | 16 bits | 0 to 65,535                   | '\u0000'| Character |
| int     | 32 bits | -2^31 to 2^31-1               | 0       | Integer   |
| long    | 64 bits | -2^63 to 2^63-1               | 0L      | Long      |
| float   | 32 bits | ±1.4E-45 to ±3.4E+38         | 0.0f    | Float     |
| double  | 64 bits | ±4.9E-324 to ±1.8E+308       | 0.0d    | Double    |

---

*Mastering data types is essential for writing efficient and bug-free Java code. Practice with different types to understand their behavior and limitations!*