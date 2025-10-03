# Variables in Java

## Introduction

Variables are fundamental building blocks in Java programming. They are containers that store data values during program execution. Think of variables as labeled boxes where you can store different types of information that your program can use and manipulate.

![Java Variables](https://raw.githubusercontent.com/github/explore/5b3600551e122a3277c2c5368af2ad5725ffa9a1/topics/java/java.png)

## What is a Variable?

A variable is a named memory location that holds a value. The value can be changed during program execution, which is why it's called a "variable" (something that varies).

```java
int age = 25;        // 'age' is a variable that stores the value 25
String name = "John"; // 'name' is a variable that stores the text "John"
```

## Variable Declaration and Initialization

### Declaration

Declaration is telling Java that you want to create a variable:

```java
int number;        // Declares a variable named 'number' of type int
String message;    // Declares a variable named 'message' of type String
double price;      // Declares a variable named 'price' of type double
```

### Initialization

Initialization is giving a variable its first value:

```java
number = 10;           // Initializes 'number' with value 10
message = "Hello";     // Initializes 'message' with value "Hello"
price = 99.99;         // Initializes 'price' with value 99.99
```

### Declaration with Initialization

You can declare and initialize in one line:

```java
int number = 10;              // Declare and initialize
String message = "Hello";     // Declare and initialize
double price = 99.99;         // Declare and initialize
boolean isActive = true;      // Declare and initialize
```

## Variable Naming Rules

### Mandatory Rules (Must Follow)

1. **Start with a letter, underscore (_), or dollar sign ($)**
   ```java
   int age = 25;        ✓ Correct
   int _count = 10;     ✓ Correct
   int $price = 100;    ✓ Correct
   int 2fast = 50;      ✗ Wrong (starts with digit)
   ```

2. **Cannot use Java reserved keywords**
   ```java
   int class = 10;      ✗ Wrong ('class' is a keyword)
   int public = 20;     ✗ Wrong ('public' is a keyword)
   int myClass = 10;    ✓ Correct
   ```

3. **Case-sensitive**
   ```java
   int age = 25;
   int Age = 30;        // Different variable than 'age'
   int AGE = 35;        // Different variable than 'age' and 'Age'
   ```

4. **No spaces allowed**
   ```java
   int my age = 25;     ✗ Wrong (contains space)
   int myAge = 25;      ✓ Correct
   int my_age = 25;     ✓ Correct
   ```

### Naming Conventions (Best Practices)

1. **Use camelCase for variables**
   ```java
   int studentAge = 20;
   String firstName = "John";
   double accountBalance = 1000.50;
   ```

2. **Use meaningful names**
   ```java
   int a = 25;              // Poor naming
   int userAge = 25;        // Good naming
   
   String s = "John";       // Poor naming
   String userName = "John"; // Good naming
   ```

3. **Constants use UPPER_SNAKE_CASE**
   ```java
   final double PI = 3.14159;
   final int MAX_USERS = 100;
   final String DATABASE_URL = "jdbc:mysql://localhost:3306/mydb";
   ```

## Types of Variables

### 1. Local Variables

Variables declared inside a method, constructor, or block.

```java
public class Example {
    public void displayInfo() {
        // Local variables
        int age = 25;                    // Local to displayInfo method
        String name = "John";            // Local to displayInfo method
        
        System.out.println(name + " is " + age + " years old");
    }
    
    public void calculate() {
        // age and name are NOT accessible here
        int result = 100;                // Local to calculate method
    }
}
```

**Characteristics:**
- Must be initialized before use
- Only accessible within the method/block where declared
- Stored in stack memory
- Destroyed when method execution completes

### 2. Instance Variables (Non-Static Fields)

Variables declared inside a class but outside any method.

```java
public class Student {
    // Instance variables
    String name;              // Default value: null
    int age;                  // Default value: 0
    double gpa;               // Default value: 0.0
    boolean isEnrolled;       // Default value: false
    
    public void displayInfo() {
        System.out.println(name + " is " + age + " years old");
    }
}
```

**Characteristics:**
- Belong to an instance (object) of the class
- Have default values
- Accessible throughout the class
- Each object has its own copy
- Stored in heap memory

### 3. Static Variables (Class Variables)

Variables declared with the `static` keyword.

```java
public class Student {
    // Static variable
    static String schoolName = "ABC University";  // Shared by all objects
    static int totalStudents = 0;                 // Shared counter
    
    // Instance variables
    String name;
    int id;
    
    public Student(String name) {
        this.name = name;
        this.id = ++totalStudents;  // Increment shared counter
    }
}
```

**Characteristics:**
- Belong to the class, not individual objects
- Shared among all instances
- Memory allocated once when class is first loaded
- Accessed using class name

### Complete Example: All Variable Types

```java
public class VariableTypesDemo {
    // Static variable
    static int classVariable = 100;
    
    // Instance variables
    int instanceVariable = 50;
    String name = "Demo";
    
    public void demonstrateVariables() {
        // Local variable
        int localVariable = 25;
        
        System.out.println("Local Variable: " + localVariable);
        System.out.println("Instance Variable: " + instanceVariable);
        System.out.println("Static Variable: " + classVariable);
    }
    
    public static void main(String[] args) {
        VariableTypesDemo demo = new VariableTypesDemo();
        demo.demonstrateVariables();
        
        // Accessing static variable without object
        System.out.println("Direct access to static: " + VariableTypesDemo.classVariable);
    }
}
```

## Variable Scope

Scope determines where a variable can be accessed in the code.

### Block Scope

```java
public class ScopeDemo {
    public void demonstrateScope() {
        int x = 10;  // Method scope
        
        if (x > 5) {
            int y = 20;  // Block scope - only within if block
            System.out.println(x);  // ✓ Can access x
            System.out.println(y);  // ✓ Can access y
        }
        
        System.out.println(x);  // ✓ Can access x
        // System.out.println(y);  // ✗ Error: y is out of scope
    }
}
```

### Method Scope

```java
public class MethodScope {
    int instanceVar = 100;  // Instance scope
    
    public void method1() {
        int localVar1 = 10;  // Local to method1
        System.out.println(localVar1);    // ✓ Accessible
        System.out.println(instanceVar);  // ✓ Accessible
    }
    
    public void method2() {
        int localVar2 = 20;  // Local to method2
        System.out.println(localVar2);    // ✓ Accessible
        System.out.println(instanceVar);  // ✓ Accessible
        // System.out.println(localVar1); // ✗ Error: not accessible
    }
}
```

### Loop Scope

```java
public class LoopScope {
    public void demonstrateLoopScope() {
        for (int i = 0; i < 5; i++) {  // 'i' has loop scope
            System.out.println(i);      // ✓ Accessible
        }
        // System.out.println(i);      // ✗ Error: i is out of scope
        
        int j;
        for (j = 0; j < 5; j++) {      // 'j' declared outside loop
            System.out.println(j);      // ✓ Accessible
        }
        System.out.println(j);          // ✓ Accessible (j = 5)
    }
}
```

## Default Values

Different variable types have different default values:

```java
public class DefaultValues {
    // Instance variables with default values
    byte byteVar;           // 0
    short shortVar;         // 0
    int intVar;             // 0
    long longVar;           // 0L
    float floatVar;         // 0.0f
    double doubleVar;       // 0.0d
    char charVar;           // '\u0000' (null character)
    boolean booleanVar;     // false
    String stringVar;       // null
    Object objectVar;       // null
    
    public void displayDefaults() {
        System.out.println("byte: " + byteVar);        // 0
        System.out.println("short: " + shortVar);      // 0
        System.out.println("int: " + intVar);          // 0
        System.out.println("long: " + longVar);        // 0
        System.out.println("float: " + floatVar);      // 0.0
        System.out.println("double: " + doubleVar);    // 0.0
        System.out.println("char: '" + charVar + "'"); // ''
        System.out.println("boolean: " + booleanVar);  // false
        System.out.println("String: " + stringVar);    // null
        System.out.println("Object: " + objectVar);    // null
    }
}
```

**Note:** Local variables do NOT have default values and must be initialized before use!

## Final Variables (Constants)

Variables declared with `final` keyword cannot be modified once initialized.

```java
public class FinalVariables {
    // Constants (static final)
    static final double PI = 3.14159;
    static final int MAX_USERS = 100;
    
    // Instance constant
    final String COUNTRY = "USA";
    
    // Blank final variable (initialized in constructor)
    final int id;
    
    public FinalVariables(int id) {
        this.id = id;  // Must initialize in constructor
    }
    
    public void demonstrateFinal() {
        final int localConstant = 50;
        // localConstant = 60;  // ✗ Error: cannot modify final variable
        
        // PI = 3.14;           // ✗ Error: cannot modify final variable
    }
}
```

## Variable Type Inference (var keyword)

Since Java 10, you can use `var` for local variable type inference:

```java
public class VarKeywordDemo {
    public void demonstrateVar() {
        // Type inference with var
        var number = 10;              // Inferred as int
        var text = "Hello";           // Inferred as String
        var price = 99.99;            // Inferred as double
        var list = new ArrayList<>(); // Inferred as ArrayList<Object>
        
        // var must be initialized at declaration
        // var x;                     // ✗ Error: cannot use var without initializer
        
        // var cannot be used for:
        // - Instance variables
        // - Method parameters
        // - Return types
    }
}
```

## Best Practices

### 1. Initialize Variables

```java
// Poor practice
int count;
// ... some code ...
count = 10;  // May forget to initialize

// Good practice
int count = 0;  // Initialize immediately
```

### 2. Use Meaningful Names

```java
// Poor naming
int d = 30;
String n = "John";
double s = 50000;

// Good naming
int daysInMonth = 30;
String userName = "John";
double annualSalary = 50000;
```

### 3. Declare Variables Close to Usage

```java
// Poor practice
public void processData() {
    int result;
    String message;
    double calculation;
    
    // ... lots of code ...
    
    result = 100;
    // ... use result
}

// Good practice
public void processData() {
    // ... some code ...
    
    int result = 100;  // Declare when needed
    // ... use result
}
```

### 4. Use Constants for Fixed Values

```java
// Poor practice
public void calculateArea() {
    double area = radius * radius * 3.14159;
}

// Good practice
public class Circle {
    private static final double PI = 3.14159;
    
    public void calculateArea() {
        double area = radius * radius * PI;
    }
}
```

## Common Mistakes and Solutions

### 1. Using Uninitialized Local Variables

```java
// ✗ Wrong
public void calculate() {
    int result;
    System.out.println(result);  // Error: variable might not have been initialized
}

// ✓ Correct
public void calculate() {
    int result = 0;
    System.out.println(result);
}
```

### 2. Scope Confusion

```java
// ✗ Wrong
public void processData() {
    if (true) {
        int data = 100;
    }
    System.out.println(data);  // Error: cannot find symbol
}

// ✓ Correct
public void processData() {
    int data;
    if (true) {
        data = 100;
    }
    System.out.println(data);
}
```

### 3. Naming Conflicts

```java
public class NamingConflict {
    int value = 10;  // Instance variable
    
    public void setValue(int value) {
        value = value;  // ✗ Wrong: assigns parameter to itself
    }
    
    public void setValueCorrect(int value) {
        this.value = value;  // ✓ Correct: uses 'this' to refer to instance variable
    }
}
```

## Variable Memory Allocation

```java
public class MemoryDemo {
    static int staticVar = 100;     // Stored in Method Area
    int instanceVar = 50;           // Stored in Heap (with object)
    
    public void method() {
        int localVar = 25;          // Stored in Stack
        Integer wrapperVar = 200;   // Object stored in Heap, reference in Stack
    }
}
```

### Memory Diagram

```
┌─────────────────┐
│   Method Area   │ ← Static variables
│  staticVar=100  │
├─────────────────┤
│      Heap       │ ← Objects & Instance variables
│ Object {        │
│  instanceVar=50 │
│ }               │
│ Integer obj=200 │
├─────────────────┤
│     Stack       │ ← Local variables & references
│ localVar=25     │
│ wrapperVar(ref) │
└─────────────────┘
```

## Practice Examples

### Example 1: Student Information System

```java
public class Student {
    // Static variable
    private static int totalStudents = 0;
    private static final String SCHOOL_NAME = "ABC School";
    
    // Instance variables
    private int studentId;
    private String name;
    private int age;
    private double gpa;
    private boolean isActive;
    
    // Constructor
    public Student(String name, int age) {
        this.studentId = ++totalStudents;
        this.name = name;
        this.age = age;
        this.gpa = 0.0;
        this.isActive = true;
    }
    
    // Method using local variables
    public void displayInfo() {
        String status = isActive ? "Active" : "Inactive";  // Local variable
        String info = String.format("ID: %d, Name: %s, Age: %d, Status: %s",
                                  studentId, name, age, status);
        System.out.println(info);
        System.out.println("School: " + SCHOOL_NAME);
    }
    
    public static void main(String[] args) {
        Student student1 = new Student("Alice", 20);
        Student student2 = new Student("Bob", 21);
        
        student1.displayInfo();
        student2.displayInfo();
        
        System.out.println("Total Students: " + totalStudents);
    }
}
```

### Example 2: Variable Scope Demonstration

```java
public class VariableScopeDemo {
    // Class variable
    private static int classLevel = 100;
    
    // Instance variable
    private int instanceLevel = 200;
    
    public void demonstrateScopes(int parameterLevel) {
        // Method level variable
        int methodLevel = 300;
        
        System.out.println("Parameter: " + parameterLevel);
        System.out.println("Method Level: " + methodLevel);
        System.out.println("Instance Level: " + instanceLevel);
        System.out.println("Class Level: " + classLevel);
        
        // Block scope
        {
            int blockLevel = 400;
            System.out.println("Block Level: " + blockLevel);
            
            // All variables accessible here
            int sum = parameterLevel + methodLevel + instanceLevel + 
                     classLevel + blockLevel;
            System.out.println("Sum of all: " + sum);
        }
        
        // blockLevel not accessible here
        // System.out.println(blockLevel); // Error!
    }
    
    public static void main(String[] args) {
        VariableScopeDemo demo = new VariableScopeDemo();
        demo.demonstrateScopes(500);
    }
}
```

## Summary

Variables are essential components of Java programming that allow you to store and manipulate data. Key points to remember:

1. **Declaration and Initialization**: Variables must be declared with a type and should be initialized before use
2. **Naming Rules**: Follow Java naming conventions for readable code
3. **Types**: Understand the differences between local, instance, and static variables
4. **Scope**: Know where your variables can be accessed
5. **Best Practices**: Use meaningful names, initialize variables, and follow conventions

## Practice Exercises

1. Create a `BankAccount` class with appropriate instance and static variables
2. Write a program demonstrating all types of variables and their scopes
3. Create a `Calculator` class that uses final variables for mathematical constants
4. Implement a `Counter` class that tracks how many objects have been created
5. Write a program that demonstrates variable shadowing and how to resolve it

---

*Understanding variables is crucial for Java programming. Master these concepts before moving on to more complex topics!*