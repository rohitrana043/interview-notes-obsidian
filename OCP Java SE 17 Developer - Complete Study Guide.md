# 📚 Table of Contents

## Core Java Fundamentals
- [[#Chapter 1 Basics of Java Programming]]
- [[#Chapter 2 Basic Elements, Primitive Data Types, and Operators]]
- [[#Chapter 3 Declarations]]
- [[#Chapter 4 Control Flow]]

## Object-Oriented Programming
- [[#Chapter 5 Object-Oriented Programming]]
- [[#Chapter 6 Access Control]]
- [[#Chapter 7 Exception Handling]]

## Java APIs and Advanced Features
- [[#Chapter 8 Selected API Classes]]
- [[#Chapter 9 Nested Type Declarations]]
- [[#Chapter 10 Object Lifetime]]
- [[#Chapter 11 Generics]]

## Collections Framework
- [[#Chapter 12 Collections, Part I ArrayList]]
- [[#Chapter 13 Functional-Style Programming]]
- [[#Chapter 14 Object Comparison]]
- [[#Chapter 15 Collections Part II]]

## Functional Programming and Streams
- [[#Chapter 16 Streams]]

## Date, Time, and Localization
- [[#Chapter 17 Date and Time]]
- [[#Chapter 18 Localization]]

## Advanced Topics
- [[#Chapter 19 Java Module System]]
- [[#Chapter 20 Java I O Part I]]
- [[#Chapter 21 Java I O Part II]]
- [[#Chapter 22 Concurrency Part I]]
- [[#Chapter 23 Concurrency Part II]]
- [[#Chapter 24 Database Connectivity]]
- [[#Chapter 25 Annotations]]
- [[#Chapter 26 Secure Coding]]

## Reference Materials
- [[#Comprehensive Interview Q&A Bank]]
- [[#Quick Reference Summary]]

## Additional Resources
- [[#Final Exam Preparation Tips]]
- [[#Version-Specific Features Summary]]
- [[#Common Pitfalls to Avoid]]
- [[#Design Pattern Templates]]
- [[#Memory Management Tips]]
- [[#Performance Optimization Checklist]]
- [[#Security Best Practices]]

---

## Chapter 1: Basics of Java Programming

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Java Ecosystem**|• JDK (Java Development Kit): Contains compiler, JRE, development tools<br>• JRE (Java Runtime Environment): JVM + core libraries<br>• JVM (Java Virtual Machine): Executes bytecode, platform-independent<br>• Write Once, Run Anywhere (WORA) principle|
|**Classes**|• Blueprint for creating objects<br>• Contains fields (state) and methods (behavior)<br>• Syntax: `public class ClassName { }`<br>• One public class per .java file<br>• File name must match public class name|
|**Objects**|• Instance of a class<br>• Created using `new` keyword<br>• Has state (instance variables) and behavior (methods)<br>• Stored in heap memory|
|**Instance Members**|• Belong to object instances<br>• Each object has its own copy<br>• Accessed via object reference<br>• Include instance variables and instance methods|
|**Static Members**|• Belong to the class itself<br>• Shared among all instances<br>• Accessed via class name<br>• Memory allocated once when class is loaded|
|**Inheritance**|• IS-A relationship<br>• `extends` keyword<br>• Single inheritance only (one superclass)<br>• All classes implicitly extend Object<br>• Promotes code reuse|
|**Aggregation**|• HAS-A relationship<br>• Composition: Strong relationship (owner manages lifecycle)<br>• Association: Weak relationship (independent lifecycles)|

### Code Examples

```java
// Class Declaration
public class Employee {
    // Instance variables
    private String name;
    private int id;
    
    // Static variable
    private static int employeeCount = 0;
    
    // Constructor
    public Employee(String name) {
        this.name = name;
        this.id = ++employeeCount;
    }
    
    // Instance method
    public String getName() {
        return name;
    }
    
    // Static method
    public static int getEmployeeCount() {
        return employeeCount;
    }
}

// Inheritance Example
public class Manager extends Employee {
    private String department;
    
    public Manager(String name, String department) {
        super(name);  // Call parent constructor
        this.department = department;
    }
}

// Aggregation Example
public class Department {
    private List<Employee> employees;  // HAS-A relationship
    
    public Department() {
        this.employees = new ArrayList<>();
    }
}
```

### Interview Q&A

**Q1: What's the difference between JDK, JRE, and JVM?**

- **JVM**: Executes bytecode, provides platform independence
- **JRE**: JVM + libraries needed to run Java applications
- **JDK**: JRE + development tools (compiler, debugger, etc.)

**Q2: Explain the difference between instance and static members.**

- Instance members belong to objects, each instance has its own copy
- Static members belong to the class, shared among all instances
- Static members loaded once when class is first referenced

**Q3: What's the difference between inheritance and composition?**

- Inheritance: IS-A relationship, extends functionality
- Composition: HAS-A relationship, contains other objects
- Favor composition over inheritance for flexibility

---

## Chapter 2: Basic Elements, Primitive Data Types, and Operators

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Primitive Types**|• byte (8 bits): -128 to 127<br>• short (16 bits): -32,768 to 32,767<br>• int (32 bits): ~-2.1 billion to 2.1 billion<br>• long (64 bits): -2^63 to 2^63-1<br>• float (32 bits): ~7 decimal digits<br>• double (64 bits): ~15 decimal digits<br>• boolean: true/false<br>• char (16 bits): Unicode character|
|**Type Conversion**|• Widening (implicit): byte → short → int → long → float → double<br>• Narrowing (explicit): Requires casting, may lose data<br>• Auto-boxing/unboxing between primitives and wrappers|
|**Operators**|• Arithmetic: +, -, *, /, %<br>• Unary: ++, --, +, -, !, ~<br>• Relational: <, >, <=, >=, ==, !=<br>• Logical: &&, \|, &, \|, ^<br>• Bitwise: &, \|, ^, ~, <<, >>, >>><br>• Assignment: =, +=, -=, *=, /=, %=<br>• Ternary: condition ? value1 : value2|
|**Operator Precedence**|1. Postfix (x++, x--)<br>2. Unary (++x, --x, +, -, !, ~)<br>3. Multiplicative (*, /, %)<br>4. Additive (+, -)<br>5. Shift (<<, >>, >>>)<br>6. Relational (<, >, <=, >=, instanceof)<br>7. Equality (==, !=)<br>8. Bitwise AND (&)<br>9. Bitwise XOR (^)<br>10. Bitwise OR (\|)<br>11. Logical AND (&&)<br>12. Logical OR (\|)<br>13. Ternary (?:)<br>14. Assignment (=, +=, -=, etc.)|
|**String Concatenation**|• + operator with strings<br>• Left-to-right evaluation<br>• Any operand with string converts result to string|

### Code Examples

```java
// Primitive Types and Literals
byte b = 127;           // byte literal
short s = 32000;        // short literal
int i = 1_000_000;      // underscore for readability
long l = 100L;          // L suffix for long
float f = 3.14F;        // F suffix for float
double d = 3.14;        // default decimal is double
boolean flag = true;    // boolean literal
char c = 'A';           // character literal
char unicode = '\u0041'; // Unicode for 'A'

// Type Conversion
int x = 100;
long y = x;             // Widening - automatic
int z = (int) y;        // Narrowing - requires cast

// Operator Examples
int a = 10, b = 3;
System.out.println(a / b);     // 3 (integer division)
System.out.println(a % b);     // 1 (remainder)
System.out.println(++a);       // 11 (pre-increment)
System.out.println(b++);       // 3 (post-increment, b is now 4)

// Bitwise Operations
int m = 5;              // 0101 in binary
int n = 3;              // 0011 in binary
System.out.println(m & n);  // 1 (0001)
System.out.println(m | n);  // 7 (0111)
System.out.println(m ^ n);  // 6 (0110)
System.out.println(~m);     // -6 (two's complement)

// String Concatenation
String result = "Value: " + 10 + 20;      // "Value: 1020"
String result2 = 10 + 20 + " Value";      // "30 Value"
```

### Interview Q&A

**Q1: What's the difference between == and equals()?**

- `==` compares references for objects, values for primitives
- `equals()` compares object content (when properly overridden)
- For strings, use `equals()` for content comparison

**Q2: Explain short-circuit evaluation in && and ||.**

- `&&`: If left operand is false, right is not evaluated
- `||`: If left operand is true, right is not evaluated
- Improves performance and prevents potential errors

**Q3: What's the difference between >> and >>>?**

- `>>`: Signed right shift, preserves sign bit
- `>>>`: Unsigned right shift, fills with zeros
- Important for bit manipulation and performance optimization

---

## Chapter 3: Declarations

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Class Declarations**|• Modifiers: public, abstract, final<br>• Only one public class per file<br>• Can have multiple non-public classes<br>• Abstract classes cannot be instantiated<br>• Final classes cannot be extended|
|**Method Declarations**|• Syntax: `[modifiers] returnType methodName(parameters)`<br>• Can be overloaded (same name, different parameters)<br>• Return type not part of signature<br>• void methods don't return values|
|**Variable Declarations**|• Local variables: Inside methods, not initialized by default<br>• Instance variables: Per object, default initialization<br>• Static variables: Per class, default initialization<br>• Final variables: Constants, must be initialized|
|**this Reference**|• Refers to current object<br>• Distinguishes instance variables from parameters<br>• Cannot be used in static context<br>• Used for constructor chaining|
|**Method Overloading**|• Same method name, different parameter list<br>• Return type alone doesn't distinguish<br>• Compile-time polymorphism<br>• Parameter type, number, or order must differ|
|**Constructors**|• Special method for object initialization<br>• Same name as class, no return type<br>• Default constructor provided if none defined<br>• Can be overloaded<br>• Called with `new` keyword|
|**Arrays**|• Fixed size, homogeneous elements<br>• Zero-indexed<br>• Length property (not method)<br>• Can be multidimensional<br>• Covariant (subtype arrays assignable to supertype array variables)|
|**Variable Arity Methods**|• Varargs: `type... paramName`<br>• Must be last parameter<br>• Only one per method<br>• Treated as array internally<br>• Can pass array or individual elements|
|**main() Method**|• Entry point: `public static void main(String[] args)`<br>• Must be public, static, void<br>• Takes String array parameter<br>• Can be overloaded but won't be entry point|
|**Local Variable Type Inference**|• `var` keyword (Java 10+)<br>• Only for local variables with initializer<br>• Not for fields, method parameters, or return types<br>• Type inferred at compile time<br>• Cannot be null initialized|

### Code Examples

```java
// Class and Method Declarations
public class Calculator {
    // Instance variable
    private double result;
    
    // Static variable
    private static int operationCount = 0;
    
    // Constructor overloading
    public Calculator() {
        this.result = 0;
    }
    
    public Calculator(double initialValue) {
        this.result = initialValue;
    }
    
    // Method overloading
    public void add(int a) {
        result += a;
        operationCount++;
    }
    
    public void add(double a) {
        result += a;
        operationCount++;
    }
    
    public void add(int a, int b) {
        result += (a + b);
        operationCount++;
    }
    
    // Varargs method
    public void addMultiple(double... values) {
        for (double value : values) {
            result += value;
        }
        operationCount++;
    }
    
    // Using 'this' reference
    public Calculator setResult(double result) {
        this.result = result;  // Distinguish field from parameter
        return this;           // Method chaining
    }
}

// Array Examples
int[] numbers = new int[5];                    // Declaration and initialization
int[] primes = {2, 3, 5, 7, 11};              // Array literal
int[][] matrix = new int[3][3];                // 2D array
int[][] jagged = {{1, 2}, {3, 4, 5}, {6}};    // Jagged array

// Local Variable Type Inference (var)
var list = new ArrayList<String>();    // Type inferred as ArrayList<String>
var stream = list.stream();            // Type inferred from method return
var number = 42;                       // Type inferred as int
// var x = null;                       // Compilation error - cannot infer type
// var y;                              // Compilation error - needs initializer

// Main method variations
public class MainExamples {
    // Standard main method
    public static void main(String[] args) {
        System.out.println("Args length: " + args.length);
    }
    
    // Valid but not entry point
    public static void main(String args) { }
    public void main(String[] args) { }
    public static int main(String[] args) { return 0; }
}
```

### Interview Q&A

**Q1: Can you overload the main method?** Yes, but only `public static void main(String[] args)` serves as the entry point. Other overloaded versions are regular methods.

**Q2: What's the difference between method overloading and overriding?**

- Overloading: Same method name, different parameters, compile-time
- Overriding: Same signature in subclass, runtime polymorphism

**Q3: When should you use var for type inference?**

- When type is obvious from initializer
- To reduce verbosity with complex generic types
- Avoid when it reduces code readability

---

## Chapter 4: Control Flow

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**if-else Statement**|• Conditional execution<br>• else is optional<br>• Can be nested<br>• Dangling else binds to nearest if|
|**switch Statement**|• Multi-way branching<br>• Works with: byte, short, int, char, String, enum<br>• Case labels must be compile-time constants<br>• break prevents fall-through<br>• default case is optional|
|**switch Expression**|• Java 14+ feature<br>• Returns a value<br>• Arrow syntax (->)<br>• No fall-through<br>• Must be exhaustive<br>• yield for complex cases|
|**while Loop**|• Pre-test loop<br>• Condition checked before execution<br>• May execute zero times<br>• Useful when iterations unknown|
|**do-while Loop**|• Post-test loop<br>• Executes at least once<br>• Condition checked after execution<br>• Semicolon required after condition|
|**for Loop**|• Counter-controlled loop<br>• Three parts: init, condition, update<br>• All parts optional<br>• Scope of init variable limited to loop|
|**Enhanced for Loop**|• For-each loop<br>• Iterates over arrays and Iterables<br>• Read-only access (can't modify structure)<br>• Simpler syntax for iteration|
|**break Statement**|• Exits innermost loop or switch<br>• Can use labels for outer loops<br>• Unconditional transfer|
|**continue Statement**|• Skips rest of current iteration<br>• Continues with next iteration<br>• Works with loops only (not switch)|
|**return Statement**|• Exits method<br>• Returns value (non-void methods)<br>• Must match method return type|

### Code Examples

```java
// Switch Statement (Traditional)
int day = 3;
String dayName;
switch (day) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
    case 4:
    case 5:
        dayName = "Weekday";
        break;
    case 6:
    case 7:
        dayName = "Weekend";
        break;
    default:
        dayName = "Invalid";
}

// Switch Expression (Java 14+)
String result = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};

// Switch Expression with yield
int numLetters = switch (day) {
    case 1, 2, 4, 5 -> 7;  // Monday, Tuesday, Thursday, Friday
    case 3 -> 9;            // Wednesday
    case 6, 7 -> {
        System.out.println("Weekend!");
        yield 8;            // Saturday, Sunday
    }
    default -> throw new IllegalArgumentException("Invalid day: " + day);
};

// Loop Examples
// Traditional for loop
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}

// Enhanced for loop
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}

// while loop
int count = 0;
while (count < 5) {
    System.out.println("Count: " + count);
    count++;
}

// do-while loop
int x = 10;
do {
    System.out.println("x: " + x);
    x--;
} while (x > 0);

// Labeled break and continue
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;  // Exits both loops
        }
        System.out.println(i + "," + j);
    }
}

// Continue example
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    System.out.println(i);  // Print odd numbers only
}
```

### Interview Q&A

**Q1: What's the difference between switch statement and switch expression?**

- Statement: Executes code, uses break, can fall through
- Expression: Returns value, uses arrow syntax, no fall through, must be exhaustive

**Q2: When would you use a do-while loop instead of a while loop?** Use do-while when the loop body must execute at least once, such as menu systems or input validation.

**Q3: Can you use continue in a switch statement?** No, continue only works with loops. In a switch, use break to exit.

---

## Chapter 5: Object-Oriented Programming

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Inheritance Implementation**|• Single inheritance with `extends`<br>• Inherit non-private members<br>• Constructor not inherited<br>• IS-A relationship test<br>• java.lang.Object is root class|
|**super Reference**|• Access parent class members<br>• Call parent constructor<br>• Must be first statement in constructor<br>• Resolve naming conflicts|
|**Constructor Chaining**|• this(): calls another constructor in same class<br>• super(): calls parent constructor<br>• Must be first statement<br>• Cannot have both this() and super()|
|**Abstract Classes**|• Cannot be instantiated<br>• Can have abstract and concrete methods<br>• Can have constructors<br>• Can have instance variables<br>• Subclasses must implement abstract methods|
|**Final Modifier**|• Final class: Cannot be extended<br>• Final method: Cannot be overridden<br>• Final variable: Cannot be reassigned<br>• Blank finals must be initialized in constructor|
|**Interfaces**|• Contract for implementation<br>• All methods public abstract (by default)<br>• Variables are public static final<br>• Multiple inheritance via interfaces<br>• Can have default and static methods (Java 8+)<br>• Can have private methods (Java 9+)|
|**Polymorphism**|• One interface, multiple implementations<br>• Compile-time: Method overloading<br>• Runtime: Method overriding<br>• Dynamic method dispatch|
|**instanceof Operator**|• Tests object type at runtime<br>• Returns boolean<br>• Pattern matching (Java 16+)<br>• Null always returns false|
|**Enum Types**|• Fixed set of constants<br>• Type-safe<br>• Can have methods and fields<br>• Implicitly final and static<br>• Cannot be extended|
|**Record Classes**|• Immutable data carriers (Java 14+)<br>• Compact constructor<br>• Automatic getters, equals, hashCode, toString<br>• Cannot extend other classes<br>• All fields are final|
|**Sealed Classes**|• Restrict inheritance (Java 17+)<br>• Permits clause specifies allowed subclasses<br>• Subclasses must be final, sealed, or non-sealed<br>• Enables exhaustive switch|

### Code Examples

```java
// Inheritance and Polymorphism
public abstract class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public abstract void makeSound();
    
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}

public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, String breed) {
        super(name);  // Call parent constructor
        this.breed = breed;
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " barks");
    }
    
    public void wagTail() {
        System.out.println(name + " wags tail");
    }
}

// Interface Example
public interface Flyable {
    // Abstract method (implicit public abstract)
    void fly();
    
    // Default method (Java 8+)
    default void glide() {
        System.out.println("Gliding through the air");
    }
    
    // Static method (Java 8+)
    static void checkWeather() {
        System.out.println("Checking weather conditions");
    }
    
    // Private method (Java 9+)
    private void adjustWings() {
        System.out.println("Adjusting wings");
    }
}

public class Bird extends Animal implements Flyable {
    public Bird(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " chirps");
    }
    
    @Override
    public void fly() {
        System.out.println(name + " is flying");
    }
}

// Enum Example
public enum DayOfWeek {
    MONDAY(1, "Start of work week"),
    TUESDAY(2, "Second day"),
    WEDNESDAY(3, "Midweek"),
    THURSDAY(4, "Almost Friday"),
    FRIDAY(5, "TGIF"),
    SATURDAY(6, "Weekend!"),
    SUNDAY(7, "Rest day");
    
    private final int dayNumber;
    private final String description;
    
    DayOfWeek(int dayNumber, String description) {
        this.dayNumber = dayNumber;
        this.description = description;
    }
    
    public boolean isWeekend() {
        return this == SATURDAY || this == SUNDAY;
    }
}

// Record Class (Java 14+)
public record Point(int x, int y) {
    // Compact constructor for validation
    public Point {
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException("Coordinates must be positive");
        }
    }
    
    // Additional method
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
}

// Sealed Classes (Java 17+)
public sealed class Shape permits Circle, Rectangle, Triangle {
    protected double area;
}

public final class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
        this.area = Math.PI * radius * radius;
    }
}

public final class Rectangle extends Shape {
    private double width, height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
        this.area = width * height;
    }
}

public non-sealed class Triangle extends Shape {
    // Can be extended further
}

// Polymorphism Example
Animal myDog = new Dog("Buddy", "Golden Retriever");
myDog.makeSound();  // Runtime polymorphism - calls Dog's makeSound()
// myDog.wagTail();  // Compilation error - not in Animal interface

if (myDog instanceof Dog dog) {  // Pattern matching (Java 16+)
    dog.wagTail();  // Now we can access Dog-specific methods
}
```

### Interview Q&A

**Q1: What's the difference between abstract class and interface?**

- Abstract class: Single inheritance, can have state, constructors, any access modifiers
- Interface: Multiple inheritance, no state (except static final), no constructors, public methods

**Q2: Explain method overriding rules.**

- Same method signature (name, parameters)
- Return type must be same or covariant
- Access modifier must be same or less restrictive
- Cannot throw broader checked exceptions

**Q3: What are the benefits of sealed classes?**

- Control inheritance hierarchy
- Enable exhaustive switch expressions
- Better API design and security
- Compiler can verify completeness

---

## Chapter 6: Access Control

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Encapsulation**|• Hide implementation details<br>• Expose only necessary interface<br>• Protect data integrity<br>• Enable maintainability|
|**Package Structure**|• Organize related classes<br>• Namespace management<br>• Package declaration first (except comments)<br>• Reverse domain naming convention|
|**Access Modifiers**|• private: Same class only<br>• default/package: Same package<br>• protected: Same package + subclasses<br>• public: Everywhere|
|**Class Path**|• Locations to search for classes<br>• Set via -cp or -classpath<br>• Current directory (.) by default<br>• Multiple paths separated by : (Unix) or ; (Windows)|
|**Scope Rules**|• Class scope: Entire class<br>• Method scope: Within method<br>• Block scope: Within block {}<br>• Inner scopes can shadow outer|
|**Immutability**|• Object state cannot change<br>• All fields final and private<br>• No setter methods<br>• Defensive copying for mutable fields<br>• Class should be final|

### Code Examples

```java
// Package Declaration and Imports
package com.company.project.model;

import java.util.List;
import java.util.ArrayList;
import static java.lang.Math.PI;
import static java.lang.Math.*;

// Access Modifiers Example
public class AccessExample {
    private int privateField = 1;      // Same class only
    int packageField = 2;               // Same package (default)
    protected int protectedField = 3;   // Same package + subclasses
    public int publicField = 4;         // Accessible everywhere
    
    private void privateMethod() { }
    void packageMethod() { }
    protected void protectedMethod() { }
    public void publicMethod() { }
}

// Immutable Class Example
public final class ImmutablePerson {
    private final String name;
    private final int age;
    private final List<String> hobbies;
    
    public ImmutablePerson(String name, int age, List<String> hobbies) {
        this.name = name;
        this.age = age;
        // Defensive copy
        this.hobbies = new ArrayList<>(hobbies);
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public List<String> getHobbies() {
        // Return defensive copy
        return new ArrayList<>(hobbies);
    }
    
    // No setter methods
}

// Scope Example
public class ScopeDemo {
    private int classField = 10;  // Class scope
    
    public void method(int parameter) {  // Method parameter scope
        int localVar = 20;  // Method scope
        
        if (true) {
            int blockVar = 30;  // Block scope
            System.out.println(classField);  // Accessible
            System.out.println(parameter);   // Accessible
            System.out.println(localVar);    // Accessible
            System.out.println(blockVar);    // Accessible
        }
        
        // System.out.println(blockVar);  // Error: out of scope
    }
    
    public void shadowingExample() {
        int classField = 100;  // Shadows class field
        System.out.println(classField);       // Prints 100
        System.out.println(this.classField);  // Prints 10
    }
}
```

### Interview Q&A

**Q1: What is the principle of encapsulation?** Encapsulation hides internal implementation details and exposes only necessary interfaces, protecting data integrity and enabling maintainability.

**Q2: Explain the different access levels in Java.**

- private: Most restrictive, same class only
- default: Same package
- protected: Same package plus subclasses anywhere
- public: Least restrictive, accessible everywhere

**Q3: How do you create an immutable class?**

1. Make class final
2. Make all fields private and final
3. No setter methods
4. Defensive copying for mutable fields
5. Initialize all fields via constructor

---

## Chapter 7: Exception Handling

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Exception Hierarchy**|• Throwable (root)<br>• Error: System errors, don't catch<br>• Exception: Application errors<br>• RuntimeException: Unchecked<br>• Others: Checked exceptions|
|**Checked vs Unchecked**|• Checked: Must handle or declare<br>• Unchecked: RuntimeException and subclasses<br>• Errors: Should not be caught|
|**try-catch-finally**|• try: Code that may throw<br>• catch: Handle specific exceptions<br>• finally: Always executes (except System.exit)<br>• Order matters: specific to general|
|**throw Statement**|• Explicitly throw exception<br>• Creates exception object<br>• Interrupts normal flow|
|**throws Clause**|• Declare checked exceptions<br>• Part of method signature<br>• Propagates to caller|
|**Multi-catch**|• Catch multiple exceptions in one block<br>• Syntax: `catch (Exception1|
|**try-with-resources**|• Automatic resource management<br>• Resources must implement AutoCloseable<br>• Closed in reverse order of creation<br>• Suppressed exceptions|

### Code Examples

```java
// Exception Hierarchy Example
public class ExceptionDemo {
    // Checked exception - must handle or declare
    public void readFile(String filename) throws IOException {
        BufferedReader reader = new BufferedReader(new FileReader(filename));
        String line = reader.readLine();
        reader.close();
    }
    
    // Unchecked exception - no need to declare
    public void divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("Cannot divide by zero");
        }
        System.out.println(a / b);
    }
    
    // Complete exception handling
    public void completeExample() {
        try {
            // Code that may throw exceptions
            readFile("data.txt");
            divide(10, 0);
        } catch (FileNotFoundException e) {
            // Specific exception first
            System.err.println("File not found: " + e.getMessage());
        } catch (IOException e) {
            // More general exception
            System.err.println("IO error: " + e.getMessage());
        } catch (ArithmeticException e) {
            // Runtime exception
            System.err.println("Math error: " + e.getMessage());
        } finally {
            // Always executes
            System.out.println("Cleanup code");
        }
    }
}

// Multi-catch (Java 7+)
public void multiCatchExample() {
    try {
        // Code that may throw multiple exceptions
        Class.forName("SomeClass");
        Thread.sleep(1000);
    } catch (ClassNotFoundException | InterruptedException e) {
        // Handle multiple exceptions
        System.err.println("Error: " + e.getMessage());
        // e is implicitly final
    }
}

// Try-with-resources (Java 7+)
public void tryWithResourcesExample(String filename) {
    // Resources are automatically closed
    try (BufferedReader reader = new BufferedReader(new FileReader(filename));
         PrintWriter writer = new PrintWriter("output.txt")) {
        
        String line;
        while ((line = reader.readLine()) != null) {
            writer.println(line.toUpperCase());
        }
    } catch (IOException e) {
        System.err.println("IO error: " + e.getMessage());
    }
    // No need for finally block to close resources
}

// Custom Exception
public class ValidationException extends Exception {
    private int errorCode;
    
    public ValidationException(String message, int errorCode) {
        super(message);
        this.errorCode = errorCode;
    }
    
    public ValidationException(String message, Throwable cause) {
        super(message, cause);
    }
    
    public int getErrorCode() {
        return errorCode;
    }
}

// Exception Propagation
public class PropagationExample {
    public void method1() throws ValidationException {
        method2();
    }
    
    public void method2() throws ValidationException {
        method3();
    }
    
    public void method3() throws ValidationException {
        throw new ValidationException("Validation failed", 400);
    }
    
    public void handleException() {
        try {
            method1();
        } catch (ValidationException e) {
            System.err.println("Caught: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Interview Q&A

**Q1: What's the difference between throw and throws?**

- throw: Statement to explicitly throw an exception
- throws: Method declaration indicating it may throw checked exceptions

**Q2: When does the finally block not execute?**

- System.exit() called
- JVM crash
- Thread death
- Infinite loop in try or catch

**Q3: What are suppressed exceptions in try-with-resources?** Exceptions thrown during resource closing that are suppressed in favor of the primary exception from the try block.

---

## Chapter 8: Selected API Classes

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Object Class**|• Root of class hierarchy<br>• Important methods: equals(), hashCode(), toString()<br>• clone(), finalize() (deprecated)<br>• wait(), notify(), notifyAll() for threading|
|**Wrapper Classes**|• Box primitives into objects<br>• Immutable<br>• Auto-boxing/unboxing<br>• Caching for common values<br>• Parsing methods (parseInt, parseDouble, etc.)|
|**String Class**|• Immutable character sequences<br>• String pool for literals<br>• Rich API for manipulation<br>• Thread-safe<br>• Concatenation creates new objects|
|**StringBuilder**|• Mutable character sequences<br>• Not thread-safe (faster)<br>• Efficient for multiple modifications<br>• StringBuffer is thread-safe alternative|
|**Math Class**|• Static utility methods<br>• Trigonometric, logarithmic, exponential<br>• Random number generation<br>• Constants: PI, E|
|**Random Class**|• Pseudo-random number generation<br>• Various distributions<br>• Seed for reproducibility<br>• ThreadLocalRandom for concurrent use|
|**BigInteger/BigDecimal**|• Arbitrary precision arithmetic<br>• Immutable<br>• Slower than primitives<br>• Essential for financial calculations|

### Code Examples

```java
// Object Class Methods
public class Person {
    private String name;
    private int age;
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && Objects.equals(name, person.name);
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

// Wrapper Classes
Integer i1 = 100;                     // Auto-boxing
int i2 = i1;                          // Auto-unboxing
Integer i3 = Integer.valueOf(100);    // Cached instance
Integer i4 = Integer.valueOf(100);
System.out.println(i3 == i4);         // true (cached)

Integer i5 = Integer.valueOf(1000);
Integer i6 = Integer.valueOf(1000);
System.out.println(i5 == i6);         // false (not cached)

// Parsing
int num = Integer.parseInt("123");
double d = Double.parseDouble("3.14");
boolean b = Boolean.parseBoolean("true");

// String Operations
String str = "Hello World";
System.out.println(str.length());              // 11
System.out.println(str.charAt(0));             // 'H'
System.out.println(str.substring(0, 5));       // "Hello"
System.out.println(str.indexOf("World"));      // 6
System.out.println(str.replace('o', 'a'));     // "Hella Warld"
System.out.println(str.toLowerCase());         // "hello world"
System.out.println(str.trim());                // Remove whitespace
System.out.println(str.startsWith("Hello"));   // true
System.out.println(str.endsWith("World"));     // true

// String Pool
String s1 = "Hello";           // String pool
String s2 = "Hello";           // Same reference
String s3 = new String("Hello"); // Heap
System.out.println(s1 == s2);  // true
System.out.println(s1 == s3);  // false
System.out.println(s1.equals(s3)); // true

// StringBuilder
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
sb.insert(5, ",");
sb.delete(5, 6);
sb.reverse();
String result = sb.toString();

// Math Class
double angle = Math.toRadians(45);
double sine = Math.sin(angle);
double cosine = Math.cos(angle);
double power = Math.pow(2, 10);        // 1024
double sqrt = Math.sqrt(16);           // 4
double random = Math.random();         // 0.0 to 1.0
int max = Math.max(10, 20);           // 20
int abs = Math.abs(-5);               // 5
long rounded = Math.round(3.7);       // 4

// Random Class
Random rand = new Random();
int randomInt = rand.nextInt(100);     // 0 to 99
double randomDouble = rand.nextDouble(); // 0.0 to 1.0
boolean randomBoolean = rand.nextBoolean();
double gaussian = rand.nextGaussian();  // Normal distribution

// BigDecimal for Precise Calculations
BigDecimal bd1 = new BigDecimal("0.1");
BigDecimal bd2 = new BigDecimal("0.2");
BigDecimal sum = bd1.add(bd2);         // Exactly 0.3
BigDecimal product = bd1.multiply(bd2);
BigDecimal quotient = bd1.divide(bd2, 10, RoundingMode.HALF_UP);

// BigInteger for Large Numbers
BigInteger bi1 = new BigInteger("12345678901234567890");
BigInteger bi2 = new BigInteger("98765432109876543210");
BigInteger biSum = bi1.add(bi2);
BigInteger biProduct = bi1.multiply(bi2);
```

### Interview Q&A

**Q1: Why is String immutable in Java?**

- Thread safety without synchronization
- String pool optimization
- Security (prevents modification of sensitive data)
- Hashcode caching for performance

**Q2: When should you use StringBuilder vs StringBuffer?**

- StringBuilder: Single-threaded, better performance
- StringBuffer: Thread-safe, synchronized methods

**Q3: What's the difference between == and equals() for strings?**

- `==`: Compares references
- `equals()`: Compares content
- Use equals() for string comparison

---

## Chapter 9: Nested Type Declarations

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Static Member Types**|• Static nested class<br>• Can access only static members of outer<br>• Can be instantiated independently<br>• Useful for helper classes|
|**Non-Static Member Classes**|• Inner class<br>• Has implicit reference to outer instance<br>• Can access all outer members<br>• Cannot have static members (except constants)|
|**Local Classes**|• Defined within method or block<br>• Can access final/effectively final local variables<br>• Not accessible outside defining scope<br>• Can be abstract or final|
|**Anonymous Classes**|• No name, declared and instantiated in one expression<br>• Implements interface or extends class<br>• Cannot have constructors<br>• Used for one-time implementations|
|**Static Local Types**|• Local class in static context<br>• No access to instance members<br>• Java 16+ allows static local classes|

### Code Examples

```java
// Static Nested Class
public class OuterClass {
    private static String staticField = "Static";
    private String instanceField = "Instance";
    
    public static class StaticNested {
        public void display() {
            System.out.println(staticField);  // Can access static
            // System.out.println(instanceField); // Error: no access
        }
    }
}

// Usage
OuterClass.StaticNested nested = new OuterClass.StaticNested();
nested.display();

// Non-Static Inner Class
public class Outer {
    private int value = 10;
    
    public class Inner {
        private int value = 20;
        
        public void printValues() {
            System.out.println("Inner value: " + value);           // 20
            System.out.println("Outer value: " + Outer.this.value); // 10
        }
    }
    
    public Inner createInner() {
        return new Inner();
    }
}

// Usage
Outer outer = new Outer();
Outer.Inner inner1 = outer.new Inner();
Outer.Inner inner2 = outer.createInner();

// Local Class
public class LocalClassExample {
    public void method() {
        final int localVar = 100;  // Must be final or effectively final
        
        class LocalClass {
            public void display() {
                System.out.println("Local var: " + localVar);
            }
        }
        
        LocalClass local = new LocalClass();
        local.display();
    }
}

// Anonymous Class
public interface Greeting {
    void greet(String name);
}

public class AnonymousExample {
    public void demonstrateAnonymous() {
        // Anonymous class implementing interface
        Greeting greeting = new Greeting() {
            @Override
            public void greet(String name) {
                System.out.println("Hello, " + name);
            }
        };
        greeting.greet("World");
        
        // Anonymous class extending abstract class
        Thread thread = new Thread() {
            @Override
            public void run() {
                System.out.println("Running in thread");
            }
        };
        thread.start();
        
        // Compare with lambda (functional interface only)
        Runnable runnable = () -> System.out.println("Lambda version");
    }
}

// Practical Example: Builder Pattern with Nested Class
public class Product {
    private final String name;
    private final double price;
    private final String category;
    
    private Product(Builder builder) {
        this.name = builder.name;
        this.price = builder.price;
        this.category = builder.category;
    }
    
    public static class Builder {
        private String name;
        private double price;
        private String category = "General";  // Default value
        
        public Builder(String name) {
            this.name = name;
        }
        
        public Builder price(double price) {
            this.price = price;
            return this;
        }
        
        public Builder category(String category) {
            this.category = category;
            return this;
        }
        
        public Product build() {
            return new Product(this);
        }
    }
}

// Usage
Product product = new Product.Builder("Laptop")
    .price(999.99)
    .category("Electronics")
    .build();
```

### Interview Q&A

**Q1: What's the difference between static and non-static nested classes?**

- Static: No implicit reference to outer, can be instantiated independently
- Non-static: Has implicit reference, needs outer instance

**Q2: When would you use an anonymous class vs a lambda?**

- Anonymous class: Multiple methods, state, extending classes
- Lambda: Single method (functional interface), stateless behavior

**Q3: Why can local classes only access final or effectively final variables?** Local classes may outlive the method execution, so they need stable values that won't change.

---

## Chapter 10: Object Lifetime

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Garbage Collection**|• Automatic memory management<br>• Removes unreachable objects<br>• Non-deterministic timing<br>• Generational collection (Young, Old, Permanent)|
|**Reachable Objects**|• Referenced from roots (stack, static fields)<br>• Transitively reachable<br>• Strong, soft, weak, phantom references|
|**Facilitating GC**|• Set references to null<br>• Exit scope for local variables<br>• Avoid memory leaks (listeners, collections)<br>• Use try-with-resources|
|**System.gc()**|• Suggests garbage collection<br>• Not guaranteed to run<br>• Generally avoid calling<br>• May impact performance|
|**Field Initializers**|• Instance: Run for each object<br>• Static: Run once when class loads<br>• Execute before constructor body|
|**Static Initializers**|• Static blocks for complex initialization<br>• Run once when class first loaded<br>• Execute in declaration order|
|**Instance Initializers**|• Instance initialization blocks<br>• Run before constructor body<br>• Useful for anonymous classes|
|**Initialization Order**|1. Static variables and blocks (parent then child)<br>2. Instance variables and blocks<br>3. Constructor body|

### Code Examples

```java
// Initialization Order Example
public class Parent {
    // 1. Static initialization (first time class is used)
    private static String parentStatic = initParentStatic();
    
    static {
        System.out.println("Parent static block");
    }
    
    // 3. Instance initialization (when object created)
    private String parentInstance = initParentInstance();
    
    {
        System.out.println("Parent instance block");
    }
    
    // 4. Constructor
    public Parent() {
        System.out.println("Parent constructor");
    }
    
    private static String initParentStatic() {
        System.out.println("Parent static field");
        return "ParentStatic";
    }
    
    private String initParentInstance() {
        System.out.println("Parent instance field");
        return "ParentInstance";
    }
}

public class Child extends Parent {
    // 2. Child static initialization
    private static String childStatic = initChildStatic();
    
    static {
        System.out.println("Child static block");
    }
    
    // 5. Child instance initialization
    private String childInstance = initChildInstance();
    
    {
        System.out.println("Child instance block");
    }
    
    // 6. Child constructor
    public Child() {
        System.out.println("Child constructor");
    }
    
    private static String initChildStatic() {
        System.out.println("Child static field");
        return "ChildStatic";
    }
    
    private String initChildInstance() {
        System.out.println("Child instance field");
        return "ChildInstance";
    }
}

// Output when creating new Child():
// Parent static field
// Parent static block
// Child static field
// Child static block
// Parent instance field
// Parent instance block
// Parent constructor
// Child instance field
// Child instance block
// Child constructor

// Garbage Collection Example
public class GCExample {
    private static List<Object> staticList = new ArrayList<>();
    
    public void demonstrateGC() {
        // Object eligible for GC after method ends
        Object localObject = new Object();
        
        // Object not eligible - referenced by static field
        Object persistentObject = new Object();
        staticList.add(persistentObject);
        
        // Making object eligible for GC
        Object temp = new Object();
        temp = null;  // Now eligible
        
        // Memory leak example - objects remain in collection
        List<byte[]> leak = new ArrayList<>();
        while (true) {
            leak.add(new byte[1024 * 1024]); // 1MB
            // Objects never removed, causing OutOfMemoryError
        }
    }
    
    // Proper resource cleanup
    public void properCleanup() {
        List<Object> tempList = new ArrayList<>();
        try {
            // Use resources
            tempList.add(new Object());
        } finally {
            tempList.clear();  // Help GC
            tempList = null;
        }
    }
}

// Complex Initialization Example
public class ComplexInit {
    private static final Map<String, String> CONFIG;
    private final List<String> instanceData;
    
    // Static initializer for complex setup
    static {
        CONFIG = new HashMap<>();
        try {
            // Load configuration
            Properties props = new Properties();
            props.load(ComplexInit.class.getResourceAsStream("/config.properties"));
            props.forEach((k, v) -> CONFIG.put(k.toString(), v.toString()));
        } catch (IOException e) {
            throw new ExceptionInInitializerError(e);
        }
    }
    
    // Instance initializer
    {
        instanceData = new ArrayList<>();
        instanceData.add("Default");
    }
    
    public ComplexInit(String... additionalData) {
        // Constructor adds to initialized list
        instanceData.addAll(Arrays.asList(additionalData));
    }
}
```

### Interview Q&A

**Q1: Can you force garbage collection in Java?** No, you can only suggest it with System.gc(). The JVM decides when to actually run GC.

**Q2: What's the initialization order for a class hierarchy?**

1. Parent static members
2. Child static members
3. Parent instance members
4. Parent constructor
5. Child instance members
6. Child constructor

**Q3: What causes memory leaks in Java?**

- Static collections holding references
- Unclosed resources
- Listener/callback registrations not removed
- Thread local variables
- Custom ClassLoader references

---

## Chapter 11: Generics

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Generic Types**|• Type parameters in angle brackets<br>• Type safety at compile time<br>• Eliminates casting<br>• Code reusability|
|**Type Parameters**|• Convention: T (Type), E (Element), K (Key), V (Value)<br>• Can have multiple: `<T, U>`<br>• Scope limited to declaration|
|**Wildcards**|• `?`: Unknown type<br>• `? extends T`: Upper bounded (covariance)<br>• `? super T`: Lower bounded (contravariance)<br>• PECS: Producer Extends, Consumer Super|
|**Bounded Type Parameters**|• `<T extends Number>`: Upper bound<br>• `<T extends A & B>`: Multiple bounds<br>• No lower bounds for type parameters|
|**Generic Methods**|• Type parameter before return type<br>• Can be static<br>• Type inference from arguments|
|**Type Erasure**|• Generics removed at runtime<br>• Replaced with bounds or Object<br>• Bridge methods for polymorphism<br>• No runtime type information|
|**Restrictions**|• No primitive type parameters<br>• No static fields of type parameter<br>• No instanceof with generics<br>• No arrays of generic types<br>• No exception types|

### Code Examples

```java
// Generic Class
public class Box<T> {
    private T content;
    
    public void set(T content) {
        this.content = content;
    }
    
    public T get() {
        return content;
    }
}

// Usage
Box<String> stringBox = new Box<>();
stringBox.set("Hello");
String value = stringBox.get();  // No casting needed

// Multiple Type Parameters
public class Pair<K, V> {
    private K key;
    private V value;
    
    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    
    public K getKey() { return key; }
    public V getValue() { return value; }
}

// Bounded Type Parameters
public class NumberBox<T extends Number> {
    private T number;
    
    public void set(T number) {
        this.number = number;
    }
    
    public double getDoubleValue() {
        return number.doubleValue();  // Can use Number methods
    }
}

// Generic Method
public class Utility {
    // Generic method with type inference
    public static <T> void swap(T[] array, int i, int j) {
        T temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
    
    // Multiple bounds
    public static <T extends Comparable<T> & Serializable> 
            T max(T first, T second) {
        return first.compareTo(second) > 0 ? first : second;
    }
}

// Wildcards Examples
public class WildcardExamples {
    // Upper bounded wildcard - can read
    public double sumNumbers(List<? extends Number> numbers) {
        double sum = 0;
        for (Number num : numbers) {
            sum += num.doubleValue();
        }
        // numbers.add(1);  // Compilation error - cannot add
        return sum;
    }
    
    // Lower bounded wildcard - can write
    public void addNumbers(List<? super Integer> list) {
        list.add(1);
        list.add(2);
        // Integer num = list.get(0);  // Compilation error - returns Object
    }
    
    // Unbounded wildcard
    public void printList(List<?> list) {
        for (Object item : list) {
            System.out.println(item);
        }
        // list.add("test");  // Compilation error - cannot add (except null)
    }
}

// PECS Principle (Producer Extends, Consumer Super)
public class Stack<E> {
    private List<E> elements = new ArrayList<>();
    
    // Producer - use extends
    public void pushAll(Iterable<? extends E> src) {
        for (E e : src) {
            elements.add(e);
        }
    }
    
    // Consumer - use super
    public void popAll(Collection<? super E> dst) {
        while (!elements.isEmpty()) {
            dst.add(elements.remove(elements.size() - 1));
        }
    }
}

// Type Erasure Example
public class TypeErasureDemo<T> {
    private T value;
    
    // After erasure, becomes:
    // private Object value;
    
    public void setValue(T value) {
        this.value = value;
    }
    // After erasure:
    // public void setValue(Object value)
}

// What you CANNOT do with generics
public class GenericRestrictions<T> {
    // private static T staticField;  // Error: no static fields
    // T[] array = new T[10];         // Error: no generic arrays
    
    public void method(Object obj) {
        // if (obj instanceof T) { }   // Error: no instanceof
        // T instance = new T();       // Error: no instantiation
    }
    
    // class MyException<T> extends Exception { }  // Error: no generic exceptions
}
```

### Interview Q&A

**Q1: What is type erasure and why does Java use it?** Type erasure removes generic type information at runtime, replacing with bounds or Object. Used for backward compatibility with pre-generics code.

**Q2: Explain PECS (Producer Extends, Consumer Super).**

- Use `? extends T` when you only read from a structure (producer)
- Use `? super T` when you only write to a structure (consumer)
- Use exact type T when you both read and write

**Q3: Why can't you create arrays of generic types?** Arrays are covariant and retain type info at runtime, while generics use type erasure. This combination would break type safety.

---

## Chapter 12: Collections, Part I: ArrayList

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**ArrayList Features**|• Dynamic resizing array<br>• Ordered collection<br>• Allows duplicates and nulls<br>• Fast random access O(1)<br>• Slow insertion/deletion O(n)|
|**Constructors**|• Empty: `new ArrayList<>()`<br>• With capacity: `new ArrayList<>(100)`<br>• From collection: `new ArrayList<>(list)`|
|**Modifying Operations**|• add(E): Append to end<br>• add(index, E): Insert at position<br>• set(index, E): Replace element<br>• remove(Object): Remove first occurrence<br>• remove(index): Remove at position<br>• clear(): Remove all|
|**Querying Operations**|• size(): Number of elements<br>• isEmpty(): Check if empty<br>• contains(Object): Check presence<br>• indexOf(Object): First occurrence<br>• get(index): Retrieve element|
|**Iteration Methods**|• Enhanced for loop<br>• Iterator<br>• ListIterator (bidirectional)<br>• forEach() method<br>• Stream API|
|**Conversion**|• toArray(): Convert to array<br>• Arrays.asList(): Fixed-size list<br>• List.of(): Immutable list|

### Code Examples

```java
// ArrayList Creation and Basic Operations
import java.util.*;

public class ArrayListDemo {
    public static void main(String[] args) {
        // Creation
        ArrayList<String> list = new ArrayList<>();
        ArrayList<Integer> numbers = new ArrayList<>(20); // Initial capacity
        
        // Adding elements
        list.add("Apple");
        list.add("Banana");
        list.add(1, "Orange");  // Insert at index 1
        
        // Modifying
        list.set(0, "Apricot"); // Replace at index 0
        
        // Removing
        list.remove("Banana");  // Remove by object
        list.remove(0);         // Remove by index
        
        // Querying
        boolean hasOrange = list.contains("Orange");
        int index = list.indexOf("Orange");
        String first = list.get(0);
        int size = list.size();
        
        // Bulk operations
        List<String> fruits = Arrays.asList("Mango", "Grape");
        list.addAll(fruits);
        list.removeAll(fruits);
        list.retainAll(Arrays.asList("Orange"));
    }
}

// Iteration Examples
public class IterationDemo {
    public static void demonstrateIteration() {
        List<String> colors = new ArrayList<>();
        colors.add("Red");
        colors.add("Green");
        colors.add("Blue");
        
        // 1. Enhanced for loop
        for (String color : colors) {
            System.out.println(color);
        }
        
        // 2. Traditional for loop
        for (int i = 0; i < colors.size(); i++) {
            System.out.println(colors.get(i));
        }
        
        // 3. Iterator
        Iterator<String> iterator = colors.iterator();
        while (iterator.hasNext()) {
            String color = iterator.next();
            if (color.equals("Green")) {
                iterator.remove();  // Safe removal during iteration
            }
        }
        
        // 4. ListIterator (bidirectional)
        ListIterator<String> listIterator = colors.listIterator();
        while (listIterator.hasNext()) {
            String color = listIterator.next();
            listIterator.set(color.toUpperCase()); // Modify during iteration
        }
        
        // 5. forEach method
        colors.forEach(System.out::println);
        
        // 6. Stream API
        colors.stream()
            .filter(c -> c.startsWith("R"))
            .forEach(System.out::println);
    }
}

// ArrayList vs Array
public class ArrayVsArrayList {
    public static void compare() {
        // Array - fixed size, primitive support
        int[] array = new int[5];
        array[0] = 10;
        int length = array.length;  // Property
        
        // ArrayList - dynamic size, objects only
        ArrayList<Integer> list = new ArrayList<>();
        list.add(10);  // Auto-boxing
        int size = list.size();  // Method
        
        // Conversion
        Integer[] arrayFromList = list.toArray(new Integer[0]);
        List<Integer> listFromArray = Arrays.asList(arrayFromList);
        
        // Performance comparison
        // Array: Faster, less memory overhead
        // ArrayList: More flexible, rich API
    }
}

// Creating Immutable Lists
public class ImmutableLists {
    public static void createImmutable() {
        // Java 9+ List.of()
        List<String> immutable1 = List.of("A", "B", "C");
        // immutable1.add("D");  // UnsupportedOperationException
        
        // Collections.unmodifiableList()
        List<String> mutable = new ArrayList<>();
        mutable.add("X");
        mutable.add("Y");
        List<String> immutable2 = Collections.unmodifiableList(mutable);
        
        // Arrays.asList() - fixed size but mutable
        List<String> fixed = Arrays.asList("P", "Q", "R");
        fixed.set(0, "Z");  // Allowed
        // fixed.add("S");  // UnsupportedOperationException
    }
}

// Practical Example: Managing a Shopping Cart
public class ShoppingCart {
    private ArrayList<Item> items;
    
    public ShoppingCart() {
        this.items = new ArrayList<>();
    }
    
    public void addItem(Item item) {
        items.add(item);
    }
    
    public void removeItem(Item item) {
        items.remove(item);
    }
    
    public double calculateTotal() {
        return items.stream()
            .mapToDouble(Item::getPrice)
            .sum();
    }
    
    public List<Item> getItems() {
        // Return defensive copy
        return new ArrayList<>(items);
    }
    
    static class Item {
        private String name;
        private double price;
        
        public Item(String name, double price) {
            this.name = name;
            this.price = price;
        }
        
        public double getPrice() { return price; }
    }
}
```

### Interview Q&A

**Q1: What's the difference between ArrayList and LinkedList?**

- ArrayList: Dynamic array, O(1) random access, O(n) insertion/deletion
- LinkedList: Doubly-linked list, O(n) access, O(1) insertion/deletion at ends

**Q2: How does ArrayList handle resizing?** When capacity is exceeded, creates new array with 50% more capacity (typically) and copies all elements.

**Q3: Is ArrayList thread-safe?** No, use Collections.synchronizedList() or CopyOnWriteArrayList for thread safety.

---

## Chapter 13: Functional-Style Programming

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Functional Interfaces**|• Single abstract method (SAM)<br>• @FunctionalInterface annotation<br>• Can have default/static methods<br>• Lambda expression target type|
|**Lambda Expressions**|• Anonymous function syntax<br>• (parameters) -> expression/body<br>• Type inference<br>• Effectively final variable capture<br>• No state, pure functions preferred|
|**Method References**|• Shorthand for lambdas<br>• Static: `Class::staticMethod`<br>• Instance: `instance::method`<br>• Constructor: `Class::new`<br>• Array: `Type[]::new`|
|**Built-in Interfaces**|• Supplier<T>: () -> T<br>• Consumer<T>: T -> void<br>• Predicate<T>: T -> boolean<br>• Function<T,R>: T -> R<br>• BiFunction<T,U,R>: (T,U) -> R|
|**Functional Composition**|• andThen(): Sequential execution<br>• compose(): Reverse order<br>• and(), or(), negate(): Logical operations|

### Code Examples

```java
// Functional Interface Definition
@FunctionalInterface
public interface Calculator {
    int calculate(int a, int b);
    
    // Can have default methods
    default int square(int x) {
        return calculate(x, x);
    }
    
    // Can have static methods
    static void printResult(int result) {
        System.out.println("Result: " + result);
    }
}

// Lambda Expressions
public class LambdaExamples {
    public static void main(String[] args) {
        // Full syntax
        Calculator add = (int a, int b) -> {
            return a + b;
        };
        
        // Type inference
        Calculator subtract = (a, b) -> a - b;
        
        // Single parameter, no parentheses
        UnaryOperator<Integer> square = x -> x * x;
        
        // No parameters
        Supplier<String> supplier = () -> "Hello";
        
        // Multiple statements
        Consumer<String> printer = message -> {
            System.out.println("Message: " + message);
            System.out.println("Length: " + message.length());
        };
        
        // Variable capture (effectively final)
        int multiplier = 10;
        Function<Integer, Integer> multiply = x -> x * multiplier;
        // multiplier = 20;  // Error: variable must be effectively final
    }
}

// Method References
public class MethodReferenceExamples {
    public static void demonstrateReferences() {
        // Static method reference
        Function<String, Integer> parser = Integer::parseInt;
        
        // Instance method reference on particular object
        String str = "Hello";
        Supplier<Integer> lengthSupplier = str::length;
        
        // Instance method reference on arbitrary object
        Function<String, String> toUpper = String::toUpperCase;
        
        // Constructor reference
        Supplier<ArrayList<String>> listFactory = ArrayList::new;
        Function<Integer, ArrayList<String>> sizedListFactory = ArrayList::new;
        
        // Array constructor reference
        Function<Integer, String[]> arrayFactory = String[]::new;
    }
}

// Built-in Functional Interfaces
import java.util.function.*;

public class BuiltInInterfaces {
    public static void demonstrateInterfaces() {
        // Supplier - no input, produces output
        Supplier<Double> randomSupplier = Math::random;
        double random = randomSupplier.get();
        
        // Consumer - accepts input, no output
        Consumer<String> printer = System.out::println;
        printer.accept("Hello");
        
        // BiConsumer - two inputs, no output
        BiConsumer<String, Integer> repeater = (str, times) -> {
            for (int i = 0; i < times; i++) {
                System.out.println(str);
            }
        };
        
        // Predicate - test condition
        Predicate<Integer> isEven = n -> n % 2 == 0;
        boolean even = isEven.test(4);
        
        // Function - transform input to output
        Function<String, Integer> stringLength = String::length;
        int length = stringLength.apply("Hello");
        
        // BiFunction - two inputs, one output
        BiFunction<Integer, Integer, Integer> max = Math::max;
        int maximum = max.apply(5, 10);
        
        // UnaryOperator - special Function where input and output are same type
        UnaryOperator<String> upperCase = String::toUpperCase;
        
        // BinaryOperator - special BiFunction where all types are same
        BinaryOperator<Integer> sum = Integer::sum;
    }
}

// Functional Composition
public class CompositionExamples {
    public static void demonstrateComposition() {
        // Function composition
        Function<Integer, Integer> doubleIt = x -> x * 2;
        Function<Integer, Integer> addTen = x -> x + 10;
        
        // andThen: doubleIt then addTen
        Function<Integer, Integer> doubleThenAdd = doubleIt.andThen(addTen);
        System.out.println(doubleThenAdd.apply(5));  // (5 * 2) + 10 = 20
        
        // compose: addTen then doubleIt
        Function<Integer, Integer> addThenDouble = doubleIt.compose(addTen);
        System.out.println(addThenDouble.apply(5));  // (5 + 10) * 2 = 30
        
        // Predicate composition
        Predicate<Integer> isPositive = x -> x > 0;
        Predicate<Integer> isEven = x -> x % 2 == 0;
        
        Predicate<Integer> isPositiveAndEven = isPositive.and(isEven);
        Predicate<Integer> isPositiveOrEven = isPositive.or(isEven);
        Predicate<Integer> isNegative = isPositive.negate();
        
        // Consumer composition
        Consumer<String> print = System.out::print;
        Consumer<String> printLine = System.out::println;
        Consumer<String> printTwice = print.andThen(printLine);
    }
}

// Practical Example: Stream Pipeline with Lambdas
public class StreamExample {
    public static void processData() {
        List<Person> people = Arrays.asList(
            new Person("Alice", 25),
            new Person("Bob", 30),
            new Person("Charlie", 35)
        );
        
        // Using lambdas in stream operations
        List<String> names = people.stream()
            .filter(p -> p.getAge() > 25)           // Predicate
            .map(Person::getName)                    // Function (method ref)
            .map(name -> name.toUpperCase())        // Function (lambda)
            .sorted()                                 // Natural ordering
            .collect(Collectors.toList());
        
        // Using custom comparator
        people.sort(Comparator.comparing(Person::getAge)
            .thenComparing(Person::getName));
    }
    
    static class Person {
        private String name;
        private int age;
        
        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
        
        public String getName() { return name; }
        public int getAge() { return age; }
    }
}
```

### Interview Q&A

**Q1: What makes a functional interface functional?** It has exactly one abstract method. Can have multiple default/static methods.

**Q2: What does "effectively final" mean?** A variable that isn't declared final but never changes after initialization. Required for lambda variable capture.

**Q3: When should you use method references vs lambdas?** Use method references when the lambda simply calls an existing method. Use lambdas for more complex logic or when parameters need transformation.

---

## Chapter 14: Object Comparison

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**equals() Method**|• Defines equality for objects<br>• Must be reflexive, symmetric, transitive<br>• Consistent and null-safe<br>• Override with hashCode()|
|**hashCode() Method**|• Returns int hash value<br>• Equal objects must have equal hash codes<br>• Used by hash-based collections<br>• Should use same fields as equals()|
|**Comparable Interface**|• Natural ordering with compareTo()<br>• Returns negative/zero/positive<br>• Consistent with equals recommended<br>• Single sorting sequence|
|**Comparator Interface**|• External comparison logic<br>• Multiple sorting strategies<br>• Functional interface<br>• Useful factory methods|
|**Objects Utility Class**|• Null-safe operations<br>• equals(), hash(), compare()<br>• requireNonNull() validation|

### Code Examples

```java
// Implementing equals() and hashCode()
public class Person {
    private String name;
    private int age;
    private String ssn;  // Social Security Number
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        
        Person person = (Person) obj;
        return Objects.equals(ssn, person.ssn);  // Compare by SSN only
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(ssn);  // Use same field as equals
    }
}

// Implementing Comparable
public class Student implements Comparable<Student> {
    private String name;
    private double gpa;
    private int id;
    
    @Override
    public int compareTo(Student other) {
        // Natural ordering by GPA (descending), then by name
        int gpaCompare = Double.compare(other.gpa, this.gpa);
        if (gpaCompare != 0) {
            return gpaCompare;
        }
        return this.name.compareTo(other.name);
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Student)) return false;
        Student student = (Student) obj;
        return id == student.id;
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}

// Multiple Comparators
public class EmployeeComparators {
    public static class Employee {
        private String name;
        private int salary;
        private LocalDate hireDate;
        
        // Getters...
    }
    
    // Different sorting strategies
    public static final Comparator<Employee> BY_NAME = 
        Comparator.comparing(Employee::getName);
    
    public static final Comparator<Employee> BY_SALARY = 
        Comparator.comparingInt(Employee::getSalary).reversed();
    
    public static final Comparator<Employee> BY_SENIORITY = 
        Comparator.comparing(Employee::getHireDate);
    
    // Composite comparator
    public static final Comparator<Employee> COMPLEX = 
        Comparator.comparing(Employee::getSalary)
            .reversed()
            .thenComparing(Employee::getHireDate)
            .thenComparing(Employee::getName);
}

// Using Comparator factory methods
public class ComparatorFactories {
    public static void demonstrateFactories() {
        List<Person> people = getPersonList();
        
        // Natural order
        people.sort(Comparator.naturalOrder());
        
        // Reverse order
        people.sort(Comparator.reverseOrder());
        
        // Null-safe comparator
        Comparator<Person> nullSafe = 
            Comparator.nullsFirst(
                Comparator.comparing(Person::getName)
            );
        
        // Chaining comparators
        people.sort(
            Comparator.comparing(Person::getAge)
                .thenComparing(Person::getName)
                .thenComparing(Person::getCity,
                    Comparator.nullsLast(Comparator.naturalOrder()))
        );
    }
}

// Objects utility class
public class ObjectsUtilityDemo {
    public static void demonstrateObjects() {
        String s1 = "Hello";
        String s2 = null;
        
        // Null-safe equals
        boolean equal = Objects.equals(s1, s2);  // false, no NPE
        
        // Null-safe toString
        String str = Objects.toString(s2, "default");  // "default"
        
        // Generate hash code
        int hash = Objects.hash("field1", 42, true);
        
        // Null checks
        String required = Objects.requireNonNull(s1, "s1 cannot be null");
        // Objects.requireNonNull(s2);  // Throws NullPointerException
        
        // Null-safe compare
        int result = Objects.compare(s1, s2, String::compareTo);
    }
}

// Common pitfalls and best practices
public class ComparisonBestPractices {
    static class Product {
        private String id;
        private String name;
        private double price;
        
        // BAD: Inconsistent with equals
        @Override
        public boolean equals(Object obj) {
            if (!(obj instanceof Product)) return false;
            Product other = (Product) obj;
            return Objects.equals(id, other.id);
        }
        
        @Override
        public int hashCode() {
            // BAD: Using different fields than equals
            return Objects.hash(name, price);
        }
    }
    
    // GOOD: Consistent implementation
    static class BetterProduct implements Comparable<BetterProduct> {
        private String id;
        private String name;
        private double price;
        
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (!(obj instanceof BetterProduct)) return false;
            BetterProduct other = (BetterProduct) obj;
            return Objects.equals(id, other.id);
        }
        
        @Override
        public int hashCode() {
            return Objects.hash(id);  // Same field as equals
        }
        
        @Override
        public int compareTo(BetterProduct other) {
            // Consistent with equals when ids are equal
            int idCompare = id.compareTo(other.id);
            if (idCompare != 0) return idCompare;
            return 0;  // Equal IDs means equal objects
        }
    }
}
```

### Interview Q&A

**Q1: What's the contract between equals() and hashCode()?** If two objects are equal according to equals(), they must have the same hash code. The reverse is not required.

**Q2: What's the difference between Comparable and Comparator?**

- Comparable: Natural ordering, internal to class, single way to sort
- Comparator: External ordering, multiple sorting strategies possible

**Q3: Why should compareTo() be consistent with equals()?** Sorted collections (TreeSet, TreeMap) use compareTo() for equality checks. Inconsistency can lead to unexpected behavior.

---

## Chapter 15: Collections: Part II

### Cornell Notes

|**Key Concepts**|**Detailed Explanations**|
|---|---|
|**Collection Hierarchy**|• Collection (root interface)<br>• List: Ordered, duplicates allowed<br>• Set: No duplicates<br>• Queue: FIFO operations<br>• Deque: Double-ended queue<br>• Map: Key-value pairs (not Collection)|
|**List Implementations**|• ArrayList: Dynamic array, fast access<br>• LinkedList: Doubly-linked, fast insertion<br>• Vector: Legacy, synchronized<br>• Stack: Legacy, LIFO|
|**Set Implementations**|• HashSet: Hash table, no order<br>• LinkedHashSet: Maintains insertion order<br>• TreeSet: Sorted, NavigableSet<br>• EnumSet: Optimized for enums|
|**Queue Implementations**|• LinkedList: Also implements Queue<br>• PriorityQueue: Heap-based priority<br>• ArrayDeque: Resizable array|
|**Map Implementations**|• HashMap: Hash table, null allowed<br>• LinkedHashMap: Maintains order<br>• TreeMap: Sorted, NavigableMap<br>• Hashtable: Legacy, synchronized<br>• EnumMap: Optimized for enum keys|
|**Collections Utility**|• Sorting, searching, shuffling<br>• Synchronization wrappers<br>• Unmodifiable wrappers<br>• Singleton collections|

### Code Examples

```java
// Set Examples
public class SetExamples {
    public static void demonstrateSets() {
        // HashSet - no order guaranteed
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Apple");
        hashSet.add("Banana");
        hashSet.add("Apple");  // Duplicate, not added
        System.out.println(hashSet.size());  // 2
        
        // LinkedHashSet - maintains insertion order
        Set<String> linkedSet = new LinkedHashSet<>();
        linkedSet.add("First");
        linkedSet.add("Second");
        linkedSet.add("Third");
        // Iteration order: First, Second, Third
        
        // TreeSet - sorted order
        Set<Integer> treeSet = new TreeSet<>();
        treeSet.add(5);
        treeSet.add(1);
        treeSet.add(3);
        // Iteration order: 1, 3, 5
        
        // NavigableSet operations
        NavigableSet<Integer> navSet = new TreeSet<>();
        navSet.addAll(Arrays.asList(1, 3, 5, 7, 9));
        
        System.out.println(navSet.lower(5));      // 3
        System.out.println(navSet.floor(5));      // 5
        System.out.println(navSet.ceiling(5));    // 5
        System.out.println(navSet.higher(5));     // 7
        System.out.println(navSet.subSet(3, 7));  // [3, 5]
        System.out.println(navSet.headSet(5));    // [1, 3]
        System.out.println(navSet.tailSet(5));    // [5, 7, 9]
    }
}

// Queue and Deque Examples
public class QueueExamples {
    public static void demonstrateQueues() {
        // Queue operations
        Queue<String> queue = new LinkedList<>();
        queue.offer("First");   // Add to end
        queue.offer("Second");
        queue.offer("Third");
        
        String head = queue.peek();     // View head, don't remove
        String removed = queue.poll();  // Remove and return head
        
        // PriorityQueue - natural ordering or comparator
        Queue<Task> priorityQueue = new PriorityQueue<>();
        priorityQueue.offer(new Task("Low", 3));
        priorityQueue.offer(new Task("High", 1));
        priorityQueue.offer(new Task("Medium", 2));
        // Polls in priority order: High, Medium, Low
        
        // Deque operations (double-ended queue)
        Deque<String> deque = new ArrayDeque<>();
        
        // Add operations
        deque.addFirst("First");
        deque.addLast("Last");
        deque.offerFirst("New First");
        deque.offerLast("New Last");
        
        // Remove operations
        String first = deque.removeFirst();
        String last = deque.removeLast();
        String pollFirst = deque.pollFirst();
        String pollLast = deque.pollLast();
        
        // Deque as Stack (LIFO)
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(1);  // addFirst
        stack.push(2);
        stack.push(3);
        Integer popped = stack.pop();  // removeFirst - returns 3
    }
    
    static class Task implements Comparable<Task> {
        String name;
        int priority;
        
        Task(String name, int priority) {
            this.name = name;
            this.priority = priority;
        }
        
        @Override
        public int compareTo(Task other) {
            return Integer.compare(this.priority, other.priority);
        }
    }
}

// Map Examples
public class MapExamples {
    public static void demonstrateMaps() {
        // HashMap - general purpose
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("One", 1);
        hashMap.put("Two", 2);
        hashMap.put(null, 0);  // Null key allowed
        hashMap.put("Three", null);  // Null value allowed
        
        // Common operations
        Integer value = hashMap.get("One");
        Integer defaultValue = hashMap.getOrDefault("Four", 4);
        hashMap.putIfAbsent("Five", 5);
        hashMap.remove("Two");
        hashMap.replace("One", 10);
        
        // Iteration
        for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
            System.out.println(entry.getKey() + " = " + entry.getValue());
        }
        
        // TreeMap - sorted by keys
        NavigableMap<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("B", 2);
        treeMap.put("A", 1);
        treeMap.put("C", 3);
        // Iteration order: A=1, B=2, C=3
        
        // NavigableMap operations
        Map.Entry<String, Integer> firstEntry = treeMap.firstEntry();
        Map.Entry<String, Integer> lastEntry = treeMap.lastEntry();
        Map.Entry<String, Integer> lowerEntry = treeMap.lowerEntry("B");
        NavigableMap<String, Integer> subMap = treeMap.subMap("A", true, "C", false);
        
        // LinkedHashMap - maintains insertion order
        Map<String, String> linkedMap = new LinkedHashMap<>();
        linkedMap.put("First", "1");
        linkedMap.put("Second", "2");
        linkedMap.put("Third", "3");
        // Iteration maintains insertion order
        
        // Compute methods
        Map<String, Integer> scores = new HashMap<>();
        scores.compute("Alice", (k, v) -> v == null ? 1 : v + 1);
        scores.computeIfAbsent("Bob", k -> 0);
        scores.computeIfPresent("Alice", (k, v) -> v * 2);
        scores.merge("Charlie", 10, Integer::sum);
    }
}

// Collections Utility Class
public class CollectionsUtilityExamples {
    public static void demonstrateUtilities() {
        List<Integer> list = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5));
        
        // Sorting
        Collections.sort(list);
        Collections.sort(list, Collections.reverseOrder());
        
        // Searching (list must be sorted)
        Collections.sort(list);
        int index = Collections.binarySearch(list, 4);
        
        // Shuffling
        Collections.shuffle(list);
        
        // Min/Max
        Integer min = Collections.min(list);
        Integer max = Collections.max(list);
        
        // Frequency
        int freq = Collections.frequency(list, 1);
        
        // Reverse
        Collections.reverse(list);
        
        // Rotate
        Collections.rotate(list, 2);  // Rotate right by 2
        
        // Fill
        Collections.fill(list, 0);  // Fill with zeros
        
        // Synchronization wrapper
        List<String> syncList = Collections.synchronizedList(new ArrayList<>());
        
        // Unmodifiable wrapper
        List<String> unmodifiable = Collections.unmodifiableList(Arrays.asList("A", "B"));
        // unmodifiable.add("C");  // UnsupportedOperationException
        
        // Singleton collections
        Set<String> singleton = Collections.singleton("Only");
        List<String> singletonList = Collections.singletonList("Only");
        Map<String, Integer> singletonMap = Collections.singletonMap("Key", 1);
        
        // Empty collections
        List<String> emptyList = Collections.emptyList();
        Set<String> emptySet = Collections.emptySet();
        Map<String, Integer> emptyMap = Collections.emptyMap();
    }
}
```

### Interview Q&A

**Q1: When would you use TreeSet vs HashSet?**

- HashSet: When you need fast O(1) operations and don't care about order
- TreeSet: When you need sorted elements or range operations

**Q2: What's the difference between HashMap and Hashtable?**

- HashMap: Not synchronized, allows nulls, better performance
- Hashtable: Legacy, synchronized, no nulls, slower

**Q3: How does HashMap handle collisions?** Uses chaining (linked lists) for collisions. In Java 8+, converts to balanced tree (red-black tree) when chain length exceeds threshold (8).

---

## Chapter 16: Streams

### Cornell Notes

| **Key Concepts**            | **Detailed Explanations**                                                                                                                                                     |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Stream Basics**           | • Sequence of elements<br>• Functional operations<br>• Lazy evaluation<br>• Can't be reused<br>• Internal iteration                                                           |
| **Stream Sources**          | • Collections: stream()<br>• Arrays: Arrays.stream()<br>• Stream.of()<br>• Stream.generate()<br>• Stream.iterate()<br>• Files.lines()                                         |
| **Intermediate Operations** | • Lazy evaluation<br>• Return new stream<br>• filter(), map(), flatMap()<br>• distinct(), sorted()<br>• limit(), skip()<br>• peek()                                           |
| **Terminal Operations**     | • Trigger processing<br>• Produce result or side effect<br>• forEach(), count()<br>• collect(), reduce()<br>• findFirst(), findAny()<br>• allMatch(), anyMatch(), noneMatch() |
| **Optional Class** | • Container for nullable values<br>• Avoid NullPointerException<br>• of(), ofNullable(), empty()<br>• isPresent(), isEmpty()<br>• get(), orElse(), orElseGet(), orElseThrow()<br>• map(), flatMap(), filter() |
| **Collectors** | • Terminal operation utilities<br>• toList(), toSet(), toMap()<br>• groupingBy(), partitioningBy()<br>• joining(), counting()<br>• summarizing, averaging<br>• reducing(), mapping() |
| **Parallel Streams** | • Multi-threaded processing<br>• parallel() method<br>• Fork/Join framework<br>• Order not guaranteed<br>• Thread-safe operations required |

### Code Examples

```java
// Stream Creation and Basic Operations
import java.util.stream.*;
import java.util.*;

public class StreamBasics {
    public static void demonstrateStreams() {
        // Creating streams
        Stream<String> empty = Stream.empty();
        Stream<String> single = Stream.of("one");
        Stream<String> multiple = Stream.of("one", "two", "three");
        
        List<String> list = Arrays.asList("a", "b", "c");
        Stream<String> fromList = list.stream();
        
        // Generate infinite streams
        Stream<Double> randoms = Stream.generate(Math::random).limit(5);
        Stream<Integer> iterate = Stream.iterate(0, n -> n + 2).limit(10);
        Stream<Integer> iterateWithPredicate = Stream.iterate(0, n -> n < 100, n -> n + 2);
        
        // Array to stream
        int[] numbers = {1, 2, 3, 4, 5};
        IntStream intStream = Arrays.stream(numbers);
    }
}

// Intermediate Operations
public class IntermediateOperations {
    public static void demonstrateOperations() {
        List<Person> people = Arrays.asList(
            new Person("Alice", 25, "Engineer"),
            new Person("Bob", 30, "Manager"),
            new Person("Charlie", 25, "Engineer"),
            new Person("David", 35, "Director"),
            new Person("Eve", 28, "Engineer")
        );
        
        // Filter - keep elements matching predicate
        List<Person> engineers = people.stream()
            .filter(p -> "Engineer".equals(p.getRole()))
            .collect(Collectors.toList());
        
        // Map - transform elements
        List<String> names = people.stream()
            .map(Person::getName)
            .collect(Collectors.toList());
        
        // FlatMap - flatten nested structures
        List<String> words = Arrays.asList("Hello World", "Java Streams");
        List<String> letters = words.stream()
            .map(s -> s.split(""))
            .flatMap(Arrays::stream)
            .distinct()
            .collect(Collectors.toList());
        
        // Sorted
        List<Person> sortedByAge = people.stream()
            .sorted(Comparator.comparing(Person::getAge))
            .collect(Collectors.toList());
        
        // Peek - debugging
        List<String> result = people.stream()
            .filter(p -> p.getAge() > 25)
            .peek(p -> System.out.println("Filtered: " + p))
            .map(Person::getName)
            .peek(name -> System.out.println("Mapped: " + name))
            .collect(Collectors.toList());
        
        // Distinct
        List<Integer> uniqueAges = people.stream()
            .map(Person::getAge)
            .distinct()
            .collect(Collectors.toList());
        
        // Skip and Limit
        List<Person> paginated = people.stream()
            .sorted(Comparator.comparing(Person::getName))
            .skip(2)  // Skip first 2
            .limit(2) // Take next 2
            .collect(Collectors.toList());
    }
    
    static class Person {
        private String name;
        private int age;
        private String role;
        
        // Constructor and getters...
        Person(String name, int age, String role) {
            this.name = name;
            this.age = age;
            this.role = role;
        }
        
        String getName() { return name; }
        int getAge() { return age; }
        String getRole() { return role; }
    }
}

// Terminal Operations
public class TerminalOperations {
    public static void demonstrateTerminals() {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        
        // Count
        long count = numbers.stream()
            .filter(n -> n % 2 == 0)
            .count();
        
        // forEach
        numbers.stream()
            .filter(n -> n > 5)
            .forEach(System.out::println);
        
        // Reduce - accumulate elements
        Optional<Integer> sum = numbers.stream()
            .reduce((a, b) -> a + b);
        
        Integer sumWithIdentity = numbers.stream()
            .reduce(0, Integer::sum);
        
        // Collect
        Set<Integer> evenSet = numbers.stream()
            .filter(n -> n % 2 == 0)
            .collect(Collectors.toSet());
        
        // Find operations
        Optional<Integer> first = numbers.stream()
            .filter(n -> n > 5)
            .findFirst();
        
        Optional<Integer> any = numbers.parallelStream()
            .filter(n -> n > 5)
            .findAny();
        
        // Match operations
        boolean allEven = numbers.stream().allMatch(n -> n % 2 == 0);
        boolean anyEven = numbers.stream().anyMatch(n -> n % 2 == 0);
        boolean noneNegative = numbers.stream().noneMatch(n -> n < 0);
        
        // Min/Max
        Optional<Integer> min = numbers.stream().min(Integer::compare);
        Optional<Integer> max = numbers.stream().max(Integer::compare);
    }
}

// Optional Usage
public class OptionalExamples {
    public static void demonstrateOptional() {
        // Creating Optionals
        Optional<String> empty = Optional.empty();
        Optional<String> present = Optional.of("Hello");
        Optional<String> nullable = Optional.ofNullable(null);
        
        // Checking presence
        if (present.isPresent()) {
            System.out.println(present.get());
        }
        
        // Better way - functional style
        present.ifPresent(System.out::println);
        
        // Default values
        String value1 = empty.orElse("Default");
        String value2 = empty.orElseGet(() -> "Computed Default");
        String value3 = empty.orElseThrow(() -> new IllegalStateException("No value"));
        
        // Transforming
        Optional<Integer> length = present.map(String::length);
        Optional<String> upperCase = present.map(String::toUpperCase);
        
        // Chaining
        Optional<String> result = Optional.of("  hello  ")
            .map(String::trim)
            .map(String::toUpperCase)
            .filter(s -> s.length() > 3);
        
        // FlatMap for nested Optionals
        Optional<Optional<String>> nested = Optional.of(Optional.of("Nested"));
        Optional<String> flattened = nested.flatMap(opt -> opt);
        
        // Or (Java 9+)
        Optional<String> alternative = empty.or(() -> Optional.of("Alternative"));
    }
    
    // Practical use in methods
    public static Optional<User> findUserById(Long id) {
        // Database lookup
        return Optional.ofNullable(database.find(id));
    }
    
    public static void processUser(Long id) {
        findUserById(id)
            .map(User::getEmail)
            .filter(email -> email.contains("@"))
            .ifPresentOrElse(
                email -> sendEmail(email),
                () -> System.out.println("No valid email found")
            );
    }
}

// Collectors
public class CollectorExamples {
    public static void demonstrateCollectors() {
        List<Employee> employees = getEmployees();
        
        // Basic collectors
        List<String> namesList = employees.stream()
            .map(Employee::getName)
            .collect(Collectors.toList());
        
        Set<String> namesSet = employees.stream()
            .map(Employee::getName)
            .collect(Collectors.toSet());
        
        // toMap
        Map<Long, String> idToName = employees.stream()
            .collect(Collectors.toMap(
                Employee::getId,
                Employee::getName
            ));
        
        // Handle duplicates in toMap
        Map<String, Employee> deptToEmployee = employees.stream()
            .collect(Collectors.toMap(
                Employee::getDepartment,
                Function.identity(),
                (existing, replacement) -> existing  // Keep first
            ));
        
        // Grouping
        Map<String, List<Employee>> byDepartment = employees.stream()
            .collect(Collectors.groupingBy(Employee::getDepartment));
        
        Map<String, Long> countByDepartment = employees.stream()
            .collect(Collectors.groupingBy(
                Employee::getDepartment,
                Collectors.counting()
            ));
        
        // Partitioning
        Map<Boolean, List<Employee>> partitioned = employees.stream()
            .collect(Collectors.partitioningBy(
                e -> e.getSalary() > 50000
            ));
        
        // Joining
        String names = employees.stream()
            .map(Employee::getName)
            .collect(Collectors.joining(", "));
        
        // Statistics
        IntSummaryStatistics stats = employees.stream()
            .collect(Collectors.summarizingInt(Employee::getSalary));
        System.out.println("Average salary: " + stats.getAverage());
        System.out.println("Max salary: " + stats.getMax());
        
        // Downstream collectors
        Map<String, Double> avgSalaryByDept = employees.stream()
            .collect(Collectors.groupingBy(
                Employee::getDepartment,
                Collectors.averagingDouble(Employee::getSalary)
            ));
        
        // Multiple level grouping
        Map<String, Map<Integer, List<Employee>>> complexGrouping = 
            employees.stream()
                .collect(Collectors.groupingBy(
                    Employee::getDepartment,
                    Collectors.groupingBy(Employee::getLevel)
                ));
    }
    
    static class Employee {
        private Long id;
        private String name;
        private String department;
        private int salary;
        private int level;
        
        // Getters...
    }
}

// Parallel Streams
public class ParallelStreamExamples {
    public static void demonstrateParallel() {
        List<Integer> numbers = IntStream.rangeClosed(1, 1000000)
            .boxed()
            .collect(Collectors.toList());
        
        // Sequential stream
        long startSeq = System.currentTimeMillis();
        double sumSeq = numbers.stream()
            .mapToDouble(Math::sqrt)
            .sum();
        long endSeq = System.currentTimeMillis();
        
        // Parallel stream
        long startPar = System.currentTimeMillis();
        double sumPar = numbers.parallelStream()
            .mapToDouble(Math::sqrt)
            .sum();
        long endPar = System.currentTimeMillis();
        
        System.out.println("Sequential: " + (endSeq - startSeq) + "ms");
        System.out.println("Parallel: " + (endPar - startPar) + "ms");
        
        // Convert between sequential and parallel
        Stream<Integer> sequential = numbers.stream();
        Stream<Integer> parallel = sequential.parallel();
        Stream<Integer> backToSeq = parallel.sequential();
        
        // Thread safety is important
        List<Integer> result = Collections.synchronizedList(new ArrayList<>());
        numbers.parallelStream()
            .forEach(result::add);  // Thread-safe
        
        // Better: use collect for parallel streams
        List<Integer> betterResult = numbers.parallelStream()
            .filter(n -> n % 2 == 0)
            .collect(Collectors.toList());  // Thread-safe
    }
}
```

### Interview Q&A

**Q1: What's the difference between intermediate and terminal operations?**
- Intermediate: Lazy, return streams, can be chained (filter, map, sorted)
- Terminal: Eager, produce result or side effect, end the stream (collect, forEach, reduce)

**Q2: When should you use parallel streams?**
Use for CPU-intensive operations on large datasets. Avoid for I/O operations, small datasets, or when order matters.

**Q3: What's the difference between findFirst() and findAny()?**
- findFirst(): Returns first element in encounter order
- findAny(): Returns any element, better for parallel streams

---

## Chapter 17: Date and Time

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **LocalDate** | • Date without time or timezone<br>• Year-month-day<br>• ISO-8601 calendar system<br>• Immutable and thread-safe |
| **LocalTime** | • Time without date or timezone<br>• Hour-minute-second-nanosecond<br>• 24-hour clock |
| **LocalDateTime** | • Combination of date and time<br>• No timezone information<br>• Most commonly used |
| **ZonedDateTime** | • Date-time with timezone<br>• Handles daylight saving time<br>• Full timezone rules |
| **Instant** | • Point on timeline<br>• Epoch seconds + nanoseconds<br>• UTC/GMT based |
| **Period** | • Date-based amount of time<br>• Years, months, days<br>• Used with LocalDate |
| **Duration** | • Time-based amount of time<br>• Hours, minutes, seconds, nanos<br>• Used with time-based objects |
| **DateTimeFormatter** | • Format and parse dates/times<br>• Predefined and custom patterns<br>• Thread-safe |

### Code Examples

```java
import java.time.*;
import java.time.format.*;
import java.time.temporal.*;

// LocalDate, LocalTime, LocalDateTime
public class DateTimeBasics {
    public static void demonstrateBasics() {
        // Creating instances
        LocalDate date = LocalDate.now();
        LocalDate specificDate = LocalDate.of(2024, 12, 25);
        LocalDate parseDate = LocalDate.parse("2024-12-25");
        
        LocalTime time = LocalTime.now();
        LocalTime specificTime = LocalTime.of(14, 30, 45);
        LocalTime parseTime = LocalTime.parse("14:30:45");
        
        LocalDateTime dateTime = LocalDateTime.now();
        LocalDateTime specific = LocalDateTime.of(2024, 12, 25, 14, 30);
        LocalDateTime combined = LocalDateTime.of(date, time);
        
        // Accessing components
        int year = date.getYear();
        Month month = date.getMonth();
        int day = date.getDayOfMonth();
        DayOfWeek dayOfWeek = date.getDayOfWeek();
        int dayOfYear = date.getDayOfYear();
        
        // Manipulation (immutable - returns new instance)
        LocalDate tomorrow = date.plusDays(1);
        LocalDate nextWeek = date.plusWeeks(1);
        LocalDate nextMonth = date.plusMonths(1);
        LocalDate lastYear = date.minusYears(1);
        
        // With methods
        LocalDate christmas = date.withMonth(12).withDayOfMonth(25);
        LocalDate firstDayOfMonth = date.withDayOfMonth(1);
        LocalDate lastDayOfYear = date.with(TemporalAdjusters.lastDayOfYear());
        
        // Temporal adjusters
        LocalDate nextMonday = date.with(TemporalAdjusters.next(DayOfWeek.MONDAY));
        LocalDate firstTuesday = date.with(TemporalAdjusters.firstInMonth(DayOfWeek.TUESDAY));
        
        // Comparisons
        boolean isBefore = date.isBefore(tomorrow);
        boolean isAfter = date.isAfter(tomorrow);
        boolean isEqual = date.isEqual(tomorrow);
        
        // Until/Between
        long daysUntil = date.until(christmas, ChronoUnit.DAYS);
        Period period = Period.between(date, christmas);
    }
}

// ZonedDateTime and TimeZones
public class TimeZoneExamples {
    public static void demonstrateTimeZones() {
        // ZoneId
        ZoneId systemZone = ZoneId.systemDefault();
        ZoneId newYork = ZoneId.of("America/New_York");
        ZoneId paris = ZoneId.of("Europe/Paris");
        
        // Get all available zones
        Set<String> allZones = ZoneId.getAvailableZoneIds();
        
        // ZonedDateTime
        ZonedDateTime nowHere = ZonedDateTime.now();
        ZonedDateTime nowInParis = ZonedDateTime.now(paris);
        
        LocalDateTime localDT = LocalDateTime.of(2024, 6, 15, 10, 0);
        ZonedDateTime zonedDT = localDT.atZone(newYork);
        
        // Converting between zones
        ZonedDateTime parisTime = zonedDT.withZoneSameInstant(paris);
        
        // Handling daylight saving time
        ZonedDateTime beforeDST = ZonedDateTime.of(
            LocalDateTime.of(2024, 3, 10, 1, 30),
            newYork
        );
        ZonedDateTime duringDST = beforeDST.plusHours(1);  // Handles DST transition
        
        // OffsetDateTime (fixed offset, no DST rules)
        OffsetDateTime offsetDT = OffsetDateTime.now();
        ZoneOffset offset = ZoneOffset.of("+05:30");
        OffsetDateTime withOffset = localDT.atOffset(offset);
    }
}

// Instant
public class InstantExamples {
    public static void demonstrateInstant() {
        // Creating instants
        Instant now = Instant.now();
        Instant epoch = Instant.EPOCH;  // 1970-01-01T00:00:00Z
        Instant fromEpochMilli = Instant.ofEpochMilli(1000000000000L);
        Instant fromEpochSecond = Instant.ofEpochSecond(1000000000);
        
        // Operations
        Instant later = now.plus(Duration.ofHours(2));
        Instant earlier = now.minus(30, ChronoUnit.MINUTES);
        
        // Conversion
        ZonedDateTime zdt = now.atZone(ZoneId.systemDefault());
        LocalDateTime ldt = LocalDateTime.ofInstant(now, ZoneId.systemDefault());
        
        // Epoch time
        long epochMilli = now.toEpochMilli();
        long epochSecond = now.getEpochSecond();
        int nano = now.getNano();
        
        // Comparison
        boolean isAfter = now.isAfter(earlier);
        boolean isBefore = now.isBefore(later);
        
        // Duration between instants
        Duration duration = Duration.between(earlier, later);
    }
}

// Period and Duration
public class PeriodDurationExamples {
    public static void demonstratePeriodDuration() {
        // Period - for dates
        Period period = Period.of(1, 6, 15);  // 1 year, 6 months, 15 days
        Period months = Period.ofMonths(3);
        Period weeks = Period.ofWeeks(2);
        Period between = Period.between(
            LocalDate.of(2024, 1, 1),
            LocalDate.of(2024, 12, 31)
        );
        
        // Using periods
        LocalDate date = LocalDate.now();
        LocalDate future = date.plus(period);
        
        // Period components
        int years = period.getYears();
        int monthsValue = period.getMonths();
        int days = period.getDays();
        long totalMonths = period.toTotalMonths();
        
        // Duration - for time
        Duration duration = Duration.ofHours(2);
        Duration minutes = Duration.ofMinutes(30);
        Duration complex = Duration.ofHours(2).plusMinutes(30).plusSeconds(45);
        Duration betweenTimes = Duration.between(
            LocalTime.of(9, 0),
            LocalTime.of(17, 30)
        );
        
        // Duration operations
        LocalTime time = LocalTime.now();
        LocalTime later = time.plus(duration);
        
        // Duration components
        long hours = duration.toHours();
        long mins = duration.toMinutes();
        long seconds = duration.getSeconds();
        int nanos = duration.getNano();
    }
}

// Formatting and Parsing
public class FormattingParsingExamples {
    public static void demonstrateFormatting() {
        LocalDateTime dateTime = LocalDateTime.now();
        
        // Predefined formatters
        String iso = dateTime.format(DateTimeFormatter.ISO_LOCAL_DATE_TIME);
        String basic = dateTime.format(DateTimeFormatter.BASIC_ISO_DATE);
        
        // Custom patterns
        DateTimeFormatter custom = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        String formatted = dateTime.format(custom);
        
        DateTimeFormatter pattern = DateTimeFormatter.ofPattern("MMMM d, yyyy 'at' h:mm a");
        String readable = dateTime.format(pattern);  // "December 25, 2024 at 2:30 PM"
        
        // Localized formatters
        DateTimeFormatter localized = DateTimeFormatter
            .ofLocalizedDateTime(FormatStyle.MEDIUM)
            .withLocale(Locale.US);
        String localizedStr = dateTime.format(localized);
        
        // Parsing
        LocalDate parsedDate = LocalDate.parse("2024-12-25");
        LocalDate customParsed = LocalDate.parse("25/12/2024", 
            DateTimeFormatter.ofPattern("dd/MM/yyyy"));
        
        // Flexible parsing
        DateTimeFormatter flexible = new DateTimeFormatterBuilder()
            .appendPattern("[yyyy-MM-dd]")
            .appendPattern("[dd/MM/yyyy]")
            .appendPattern("[MM-dd-yyyy]")
            .toFormatter();
    }
}

// Practical Examples
public class PracticalDateTimeExamples {
    // Calculate age
    public static int calculateAge(LocalDate birthDate) {
        return Period.between(birthDate, LocalDate.now()).getYears();
    }
    
    // Business days calculation
    public static long businessDaysBetween(LocalDate start, LocalDate end) {
        return start.datesUntil(end)
            .filter(date -> {
                DayOfWeek day = date.getDayOfWeek();
                return day != DayOfWeek.SATURDAY && day != DayOfWeek.SUNDAY;
            })
            .count();
    }
    
    // Meeting scheduler
    public static ZonedDateTime scheduleMeeting(
            LocalDateTime meetingTime, 
            ZoneId organizerZone, 
            ZoneId participantZone) {
        ZonedDateTime organizerTime = meetingTime.atZone(organizerZone);
        return organizerTime.withZoneSameInstant(participantZone);
    }
    
    // Flight duration calculator
    public static Duration flightDuration(
            ZonedDateTime departure, 
            ZonedDateTime arrival) {
        return Duration.between(departure.toInstant(), arrival.toInstant());
    }
}
```

### Interview Q&A

**Q1: What's the difference between Period and Duration?**
- Period: Date-based (years, months, days), used with LocalDate
- Duration: Time-based (hours, minutes, seconds), used with time objects

**Q2: Why use Instant over LocalDateTime?**
Instant represents a point on the timeline in UTC, ideal for timestamps and system events. LocalDateTime has no timezone context.

**Q3: How do you handle daylight saving time?**
Use ZonedDateTime which automatically handles DST transitions based on timezone rules. Avoid LocalDateTime for DST-sensitive operations.

---

## Chapter 18: Localization

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Locale** | • Language + Country + Variant<br>• Format: language_COUNTRY<br>• Examples: en_US, fr_FR<br>• Controls formatting behavior |
| **ResourceBundle** | • Externalize text and resources<br>• Properties files or classes<br>• Hierarchy and fallback mechanism<br>• Locale-specific versions |
| **Number Formatting** | • NumberFormat class<br>• Currency, percentage, numbers<br>• Locale-specific formatting<br>• Parsing capabilities |
| **Date/Time Formatting** | • DateTimeFormatter<br>• Localized patterns<br>• FormatStyle options<br>• Custom patterns |
| **Message Formatting** | • MessageFormat class<br>• Placeholders and arguments<br>• Complex message patterns<br>• Choice formats |

### Code Examples

```java
import java.util.*;
import java.text.*;
import java.time.*;
import java.time.format.*;

// Locale Basics
public class LocaleExamples {
    public static void demonstrateLocales() {
        // Creating Locales
        Locale us = Locale.US;
        Locale france = Locale.FRANCE;
        Locale spanish = new Locale("es");
        Locale mexico = new Locale("es", "MX");
        Locale custom = new Locale.Builder()
            .setLanguage("en")
            .setRegion("US")
            .setVariant("POSIX")
            .build();
        
        // Default locale
        Locale defaultLocale = Locale.getDefault();
        Locale.setDefault(Locale.CANADA_FRENCH);
        
        // Available locales
        Locale[] available = Locale.getAvailableLocales();
        
        // Locale information
        String language = us.getLanguage();        // "en"
        String country = us.getCountry();          // "US"
        String displayName = us.getDisplayName();  // "English (United States)"
        String displayLanguage = us.getDisplayLanguage(france); // "anglais"
    }
}

// ResourceBundle
public class ResourceBundleExamples {
    public static void demonstrateResourceBundles() {
        // Properties files:
        // messages.properties (default)
        // messages_en.properties
        // messages_en_US.properties
        // messages_fr.properties
        // messages_fr_FR.properties
        
        Locale locale = Locale.FRANCE;
        ResourceBundle bundle = ResourceBundle.getBundle("messages", locale);
        
        // Getting values
        String greeting = bundle.getString("greeting");
        String farewell = bundle.getString("farewell");
        
        // With fallback
        ResourceBundle.Control control = ResourceBundle.Control.getControl(
            ResourceBundle.Control.FORMAT_DEFAULT
        );
        
        // Custom resource bundle loading
        ResourceBundle customBundle = ResourceBundle.getBundle(
            "config",
            locale,
            Thread.currentThread().getContextClassLoader(),
            control
        );
        
        // Iterating keys
        Enumeration<String> keys = bundle.getKeys();
        while (keys.hasMoreElements()) {
            String key = keys.nextElement();
            System.out.println(key + " = " + bundle.getString(key));
        }
    }
}

// Example properties files content:
/*
messages.properties:
greeting=Hello
farewell=Goodbye

messages_fr.properties:
greeting=Bonjour
farewell=Au revoir

messages_fr_FR.properties:
greeting=Bonjour
farewell=À bientôt
*/

// Number Formatting
public class NumberFormattingExamples {
    public static void demonstrateNumberFormatting() {
        double number = 1234567.89;
        
        // Number formatting
        NumberFormat usNumber = NumberFormat.getNumberInstance(Locale.US);
        NumberFormat frNumber = NumberFormat.getNumberInstance(Locale.FRANCE);
        
        System.out.println(usNumber.format(number));  // 1,234,567.89
        System.out.println(frNumber.format(number));  // 1 234 567,89
        
        // Currency formatting
        double amount = 9999.99;
        NumberFormat usCurrency = NumberFormat.getCurrencyInstance(Locale.US);
        NumberFormat jpCurrency = NumberFormat.getCurrencyInstance(Locale.JAPAN);
        NumberFormat euCurrency = NumberFormat.getCurrencyInstance(Locale.GERMANY);
        
        System.out.println(usCurrency.format(amount));  // $9,999.99
        System.out.println(jpCurrency.format(amount));  // ¥10,000
        System.out.println(euCurrency.format(amount));  // 9.999,99 €
        
        // Percentage formatting
        double percent = 0.75;
        NumberFormat usPercent = NumberFormat.getPercentInstance(Locale.US);
        System.out.println(usPercent.format(percent));  // 75%
        
        // Custom number format
        DecimalFormat customFormat = new DecimalFormat("#,###.00");
        customFormat.setGroupingSize(3);
        System.out.println(customFormat.format(number));
        
        // Parsing
        try {
            Number parsed = usNumber.parse("1,234,567.89");
            double value = parsed.doubleValue();
        } catch (ParseException e) {
            e.printStackTrace();
        }
        
        // Compact number formatting (Java 12+)
        NumberFormat shortFormat = NumberFormat.getCompactNumberInstance(
            Locale.US, NumberFormat.Style.SHORT
        );
        System.out.println(shortFormat.format(1000));     // 1K
        System.out.println(shortFormat.format(1000000));  // 1M
    }
}

// Date/Time Localization
public class DateTimeLocalization {
    public static void demonstrateDateTimeFormatting() {
        LocalDateTime dateTime = LocalDateTime.of(2024, 12, 25, 14, 30);
        ZonedDateTime zoned = ZonedDateTime.of(dateTime, ZoneId.systemDefault());
        
        // Localized date formatters
        DateTimeFormatter usDate = DateTimeFormatter
            .ofLocalizedDate(FormatStyle.FULL)
            .withLocale(Locale.US);
        DateTimeFormatter frDate = DateTimeFormatter
            .ofLocalizedDate(FormatStyle.FULL)
            .withLocale(Locale.FRANCE);
        
        System.out.println(dateTime.format(usDate));  
        // Wednesday, December 25, 2024
        System.out.println(dateTime.format(frDate));  
        // mercredi 25 décembre 2024
        
        // Localized time formatters
        DateTimeFormatter usTime = DateTimeFormatter
            .ofLocalizedTime(FormatStyle.SHORT)
            .withLocale(Locale.US);
        DateTimeFormatter deTime = DateTimeFormatter
            .ofLocalizedTime(FormatStyle.SHORT)
            .withLocale(Locale.GERMANY);
        
        System.out.println(dateTime.format(usTime));  // 2:30 PM
        System.out.println(dateTime.format(deTime));  // 14:30
        
        // Combined date-time
        DateTimeFormatter combined = DateTimeFormatter
            .ofLocalizedDateTime(FormatStyle.MEDIUM, FormatStyle.SHORT)
            .withLocale(Locale.UK);
        
        // Pattern with locale
        DateTimeFormatter pattern = DateTimeFormatter
            .ofPattern("EEEE, MMMM d, yyyy", Locale.FRANCE);
        System.out.println(dateTime.format(pattern));
        // mercredi, décembre 25, 2024
    }
}

// Message Formatting
public class MessageFormattingExamples {
    public static void demonstrateMessageFormatting() {
        // Simple message format
        String pattern = "Hello {0}, you have {1} new messages.";
        MessageFormat formatter = new MessageFormat(pattern);
        Object[] args = {"Alice", 5};
        String result = formatter.format(args);
        System.out.println(result);  // Hello Alice, you have 5 new messages.
        
        // With locale
        String patternFr = "Bonjour {0}, vous avez {1} nouveaux messages.";
        MessageFormat frFormatter = new MessageFormat(patternFr, Locale.FRANCE);
        
        // Complex pattern with types
        String complex = "At {0,time,short} on {0,date,long}, {1} sent {2,number,currency}.";
        MessageFormat complexFormat = new MessageFormat(complex, Locale.US);
        Object[] complexArgs = {
            new Date(),
            "John",
            1234.56
        };
        System.out.println(complexFormat.format(complexArgs));
        
        // Choice format
        String choicePattern = "There {0,choice,0#are no files|1#is one file|1<are {0,number,integer} files}.";
        MessageFormat choiceFormat = new MessageFormat(choicePattern);
        
        System.out.println(choiceFormat.format(new Object[]{0}));  // are no files
        System.out.println(choiceFormat.format(new Object[]{1}));  // is one file
        System.out.println(choiceFormat.format(new Object[]{5}));  // are 5 files
        
        // Using ResourceBundle with MessageFormat
        ResourceBundle bundle = ResourceBundle.getBundle("messages", Locale.US);
        String template = bundle.getString("welcome.message");
        // welcome.message=Welcome {0}, today is {1,date,full}
        MessageFormat bundleFormat = new MessageFormat(template, Locale.US);
        String formatted = bundleFormat.format(new Object[]{"Bob", new Date()});
    }
}

// Practical Localization Example
public class LocalizationApplication {
    private Locale currentLocale;
    private ResourceBundle messages;
    private NumberFormat currencyFormat;
    private DateTimeFormatter dateFormat;
    
    public LocalizationApplication(Locale locale) {
        this.currentLocale = locale;
        this.messages = ResourceBundle.getBundle("app_messages", locale);
        this.currencyFormat = NumberFormat.getCurrencyInstance(locale);
        this.dateFormat = DateTimeFormatter
            .ofLocalizedDate(FormatStyle.MEDIUM)
            .withLocale(locale);
    }
    
    public void displayProduct(Product product) {
        System.out.println(messages.getString("product.name") + ": " + product.getName());
        System.out.println(messages.getString("product.price") + ": " + 
            currencyFormat.format(product.getPrice()));
        System.out.println(messages.getString("product.available") + ": " + 
            product.getAvailableDate().format(dateFormat));
    }
    
    public void changeLocale(Locale newLocale) {
        this.currentLocale = newLocale;
        this.messages = ResourceBundle.getBundle("app_messages", newLocale);
        this.currencyFormat = NumberFormat.getCurrencyInstance(newLocale);
        this.dateFormat = DateTimeFormatter
            .ofLocalizedDate(FormatStyle.MEDIUM)
            .withLocale(newLocale);
    }
}

class Product {
    private String name;
    private double price;
    private LocalDate availableDate;
    
    // Constructor and getters...
}
```

### Interview Q&A

**Q1: How does ResourceBundle handle fallback?**
It searches in order: locale_COUNTRY_VARIANT, locale_COUNTRY, locale, default bundle, then throws MissingResourceException.

**Q2: What's the difference between NumberFormat and DecimalFormat?**
NumberFormat is abstract and locale-aware. DecimalFormat is concrete implementation with pattern support.

**Q3: How do you handle missing translations?**
Use try-catch with MissingResourceException, provide default values, or implement custom ResourceBundle.Control.

---

## Chapter 19: Java Module System

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Module** | • Named, self-describing collection of code<br>• Explicit dependencies<br>• Strong encapsulation<br>• Defined in module-info.java |
| **module-info.java** | • Module descriptor<br>• Declares module name<br>• Specifies dependencies (requires)<br>• Exports packages<br>• Provides services |
| **Module Directives** | • requires: Dependencies<br>• exports: Public API<br>• opens: Reflection access<br>• uses: Service consumer<br>• provides...with: Service provider |
| **Module Types** | • Named: Explicit module<br>• Automatic: JAR on module path<br>• Unnamed: Classpath compatibility |
| **jlink** | • Create custom runtime images<br>• Include only required modules<br>• Reduce application size<br>• Improve startup time |

### Code Examples

```java
// module-info.java for a simple module
module com.example.myapp {
    // Dependencies
    requires java.base;        // Implicit
    requires java.sql;
    requires java.logging;
    requires transitive com.example.common;  // Transitive dependency
    
    // Exports - public API
    exports com.example.myapp.api;
    exports com.example.myapp.model;
    exports com.example.myapp.internal to com.example.test;  // Qualified export
    
    // Opens for reflection
    opens com.example.myapp.entities;
    opens com.example.myapp.config to spring.core;
    
    // Services
    uses com.example.service.PaymentService;
    provides com.example.service.PaymentService 
        with com.example.myapp.impl.CreditCardPayment;
}

// Project structure
/*
myapp/
├── src/
│   ├── module-info.java
│   └── com/
│       └── example/
│           └── myapp/
│               ├── api/
│               │   └── PublicAPI.java
│               ├── internal/
│               │   └── InternalImpl.java
│               └── Main.java
└── out/
*/

// Service Provider Interface (SPI)
// Service interface (in API module)
public interface DataProcessor {
    void process(String data);
    String getName();
}

// Service provider (in implementation module)
public class JsonProcessor implements DataProcessor {
    @Override
    public void process(String data) {
        System.out.println("Processing JSON: " + data);
    }
    
    @Override
    public String getName() {
        return "JSON Processor";
    }
}

// module-info.java for provider
module com.example.json {
    requires com.example.api;
    provides com.example.api.DataProcessor 
        with com.example.json.JsonProcessor;
}

// Service consumer
module com.example.consumer {
    requires com.example.api;
    uses com.example.api.DataProcessor;
}

// Using services
public class ServiceConsumer {
    public static void useServices() {
        ServiceLoader<DataProcessor> processors = 
            ServiceLoader.load(DataProcessor.class);
        
        for (DataProcessor processor : processors) {
            System.out.println("Found: " + processor.getName());
            processor.process("sample data");
        }
    }
}

// Compilation and Running
/*
# Compile modules
javac -d out --module-source-path src $(find src -name "*.java")

# Run application
java --module-path out --module com.example.myapp/com.example.myapp.Main

# Create JAR
jar --create --file mods/myapp.jar \
    --main-class=com.example.myapp.Main \
    -C out/com.example.myapp .

# Run from JAR
java --module-path mods --module com.example.myapp
*/

// Migration strategies
public class MigrationExamples {
    // Automatic modules - JARs on module path
    // Manifest: Automatic-Module-Name: com.legacy.lib
    
    // Split packages handling
    // Use --patch-module to merge split packages
    
    // Unnamed module - everything on classpath
    // Can read all modules but not vice versa
}

// Creating custom runtime with jlink
/*
# List modules
java --list-modules

# Create custom runtime
jlink --module-path $JAVA_HOME/jmods:mods \
      --add-modules com.example.myapp \
      --output myapp-runtime \
      --launcher myapp=com.example.myapp/com.example.myapp.Main \
      --compress 2 \
      --strip-debug \
      --no-header-files \
      --no-man-pages

# Run with custom runtime
myapp-runtime/bin/myapp
*/

// Module reflection and runtime behavior
public class ModuleReflection {
    public static void examineModules() {
        // Get module of a class
        Module module = String.class.getModule();
        System.out.println("Module: " + module.getName());
        
        // Module descriptor
        ModuleDescriptor descriptor = module.getDescriptor();
        
        // Requires
        descriptor.requires().forEach(req -> 
            System.out.println("Requires: " + req.name())
        );
        
        // Exports
        descriptor.exports().forEach(exp -> 
            System.out.println("Exports: " + exp.source())
        );
        
        // Check if package is exported
        boolean isExported = module.isExported("java.lang");
        
        // Add exports at runtime (not recommended)
        // module.addExports("com.example.internal", targetModule);
        
        // Module layer
        ModuleLayer layer = ModuleLayer.boot();
        Optional<Module> found = layer.findModule("java.base");
    }
}

// Common module patterns
public class ModulePatterns {
    // 1. API and Implementation separation
    /*
    api-module/
        - Interfaces and contracts
        - No implementation
    
    impl-module/
        - requires api-module
        - provides services
    */
    
    // 2. Aggregator module
    /*
    module com.app.all {
        requires transitive com.app.core;
        requires transitive com.app.ui;
        requires transitive com.app.data;
    }
    */
    
    // 3. Test module
    /*
    module com.app.test {
        requires com.app.main;
        requires org.junit.jupiter.api;
        
        opens com.app.test to org.junit.platform.commons;
    }
    */
}
```

### Interview Q&A

**Q1: What problems does the module system solve?**
- JAR hell and classpath issues
- Lack of strong encapsulation
- Missing explicit dependencies
- Large runtime footprint

**Q2: What's the difference between requires and requires transitive?**
- requires: Direct dependency only
- requires transitive: Dependency is also available to modules that require this module

**Q3: How do automatic modules work?**
JARs placed on module path become automatic modules. Module name derived from JAR name or Automatic-Module-Name manifest entry.

---

## Chapter 20: Java I/O: Part I

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Byte Streams** | • InputStream/OutputStream hierarchies<br>• Handle binary data<br>• Read/write bytes<br>• Low-level I/O |
| **Character Streams** | • Reader/Writer hierarchies<br>• Handle text data<br>• Character encoding aware<br>• Higher-level than byte streams |
| **Buffering** | • BufferedInputStream/BufferedOutputStream<br>• BufferedReader/BufferedWriter<br>• Improves performance<br>• Reduces system calls |
| **Console I/O** | • System.in/out/err<br>• Console class<br>• Scanner for input<br>• PrintStream/PrintWriter for output |
| **Serialization** | • ObjectInputStream/ObjectOutputStream<br>• Serializable interface<br>• transient keyword<br>• serialVersionUID |

### Code Examples

```java
import java.io.*;

// Byte Streams
public class ByteStreamExamples {
    public static void demonstrateByteStreams() throws IOException {
        // FileInputStream/FileOutputStream
        try (FileInputStream fis = new FileInputStream("input.dat");
             FileOutputStream fos = new FileOutputStream("output.dat")) {
            
            int byteData;
            while ((byteData = fis.read()) != -1) {
                fos.write(byteData);
            }
        }
        
        // BufferedInputStream/BufferedOutputStream
        try (BufferedInputStream bis = new BufferedInputStream(
                new FileInputStream("large.dat"));
             BufferedOutputStream bos = new BufferedOutputStream(
                new FileOutputStream("copy.dat"))) {
            
            byte[] buffer = new byte[8192];
            int bytesRead;
            while ((bytesRead = bis.read(buffer)) != -1) {
                bos.write(buffer, 0, bytesRead);
            }
        }
        
        // DataInputStream/DataOutputStream
        try (DataOutputStream dos = new DataOutputStream(
                new FileOutputStream("data.bin"))) {
            dos.writeInt(42);
            dos.writeDouble(3.14159);
            dos.writeUTF("Hello World");
        }
        
        try (DataInputStream dis = new DataInputStream(
                new FileInputStream("data.bin"))) {
            int intValue = dis.readInt();
            double doubleValue = dis.readDouble();
            String stringValue = dis.readUTF();
        }
        
        // ByteArrayInputStream/ByteArrayOutputStream
        byte[] data = "Hello".getBytes();
        ByteArrayInputStream bais = new ByteArrayInputStream(data);
        
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        baos.write("World".getBytes());
        byte[] result = baos.toByteArray();
    }
}

// Character Streams
public class CharacterStreamExamples {
    public static void demonstrateCharacterStreams() throws IOException {
        // FileReader/FileWriter
        try (FileReader reader = new FileReader("text.txt");
             FileWriter writer = new FileWriter("copy.txt")) {
            
            int charData;
            while ((charData = reader.read()) != -1) {
                writer.write(charData);
            }
        }
        
        // BufferedReader/BufferedWriter
        try (BufferedReader br = new BufferedReader(new FileReader("input.txt"));
             BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            
            String line;
            while ((line = br.readLine()) != null) {
                bw.write(line);
                bw.newLine();
            }
        }
        
        // Character encoding
        try (InputStreamReader isr = new InputStreamReader(
                new FileInputStream("utf8.txt"), "UTF-8");
             OutputStreamWriter osw = new OutputStreamWriter(
                new FileOutputStream("utf16.txt"), "UTF-16")) {
            
            int c;
            while ((c = isr.read()) != -1) {
                osw.write(c);
            }
        }
        
        // StringReader/StringWriter
        String input = "Test string";
        StringReader sr = new StringReader(input);
        
        StringWriter sw = new StringWriter();
        sw.write("Output");
        String output = sw.toString();
        
        // PrintWriter
        try (PrintWriter pw = new PrintWriter(new FileWriter("print.txt"))) {
            pw.println("Line 1");
            pw.printf("Formatted: %d, %.2f%n", 42, 3.14159);
            pw.print("No newline");
        }
    }
}

// Console I/O
public class ConsoleIOExamples {
    public static void demonstrateConsoleIO() {
        // Using System.out/err
        System.out.println("Standard output");
        System.err.println("Error output");
        
        // Using Scanner for input
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter name: ");
        String name = scanner.nextLine();
        System.out.print("Enter age: ");
        int age = scanner.nextInt();
        
        // Using Console (not available in IDEs)
        Console console = System.console();
        if (console != null) {
            String username = console.readLine("Username: ");
            char[] password = console.readPassword("Password: ");
            console.printf("Hello %s!%n", username);
            // Clear password from memory
            Arrays.fill(password, ' ');
        }
        
        // Redirecting streams
        try {
            PrintStream fileOut = new PrintStream("output.log");
            System.setOut(fileOut);
            System.out.println("This goes to file");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}

// Serialization
public class SerializationExamples {
    // Serializable class
    static class Person implements Serializable {
        private static final long serialVersionUID = 1L;
        
        private String name;
        private int age;
        private transient String password;  // Not serialized
        
        public Person(String name, int age, String password) {
            this.name = name;
            this.age = age;
            this.password = password;
        }
        
        // Custom serialization
        private void writeObject(ObjectOutputStream oos) throws IOException {
            oos.defaultWriteObject();
            // Custom logic
            oos.writeObject(encrypt(password));
        }
        
        private void readObject(ObjectInputStream ois) 
                throws IOException, ClassNotFoundException {
            ois.defaultReadObject();
            // Custom logic
            password = decrypt((String) ois.readObject());
        }
        
        private String encrypt(String s) { return s; }  // Placeholder
        private String decrypt(String s) { return s; }  // Placeholder
    }
    
    public static void demonstrateSerialization() throws IOException, ClassNotFoundException {
        // Serialize object
        Person person = new Person("Alice", 30, "secret");
        
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("person.ser"))) {
            oos.writeObject(person);
        }
        
        // Deserialize object
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("person.ser"))) {
            Person restored = (Person) ois.readObject();
            System.out.println(restored.name);  // Alice
            System.out.println(restored.password);  // null (transient)
        }
        
        // Serialize collection
        List<Person> people = Arrays.asList(
            new Person("Bob", 25, "pass1"),
            new Person("Charlie", 35, "pass2")
        );
        
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("people.ser"))) {
            oos.writeObject(people);
        }
        
        // Deserialize collection
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("people.ser"))) {
            @SuppressWarnings("unchecked")
            List<Person> restoredPeople = (List<Person>) ois.readObject();
        }
    }
}

// Practical I/O Examples
public class PracticalIOExamples {
    // Copy file with progress
    public static void copyFileWithProgress(File source, File dest) 
            throws IOException {
        long totalBytes = source.length();
        long copiedBytes = 0;
        
        try (BufferedInputStream bis = new BufferedInputStream(
                new FileInputStream(source));
             BufferedOutputStream bos = new BufferedOutputStream(
                new FileOutputStream(dest))) {
            
            byte[] buffer = new byte[8192];
            int bytesRead;
            
            while ((bytesRead = bis.read(buffer)) != -1) {
                bos.write(buffer, 0, bytesRead);
                copiedBytes += bytesRead;
                
                int progress = (int) ((copiedBytes * 100) / totalBytes);
                System.out.printf("\rProgress: %d%%", progress);
            }
            System.out.println("\nCopy complete!");
        }
    }
    
    // Read configuration file
    public static Properties readConfig(String filename) throws IOException {
        Properties props = new Properties();
        try (FileInputStream fis = new FileInputStream(filename)) {
            props.load(fis);
        }
        return props;
    }
    
    // Log writer with rotation
    public static class LogWriter implements AutoCloseable {
        private PrintWriter writer;
        private long maxSize;
        private File logFile;
        
        public LogWriter(String filename, long maxSize) throws IOException {
            this.logFile = new File(filename);
            this.maxSize = maxSize;
            this.writer = new PrintWriter(new FileWriter(logFile, true));
        }
        
        public void log(String message) {
            if (logFile.length() > maxSize) {
                rotate();
            }
            writer.println(LocalDateTime.now() + " - " + message);
            writer.flush();
        }
        
        private void rotate() {
            // Implementation for log rotation
        }
        
        @Override
        public void close() {
            writer.close();
        }
    }
}
```

### Interview Q&A

**Q1: What's the difference between byte streams and character streams?**
- Byte streams: Handle binary data, 8-bit bytes
- Character streams: Handle text data, 16-bit Unicode characters with encoding support

**Q2: Why use buffered streams?**
Reduce number of system calls by reading/writing larger chunks, significantly improving I/O performance.

**Q3: What makes a class serializable?**
Implement Serializable interface, have serialVersionUID, ensure all fields are serializable or marked transient.

---

## Chapter 21: Java I/O: Part II

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Path Interface** | • Represents file system path<br>• Platform independent<br>• Immutable<br>• Rich manipulation methods |
| **Files Class** | • Static utility methods<br>• File operations<br>• Stream operations<br>• Attribute management |
| **File Attributes** | • Basic, DOS, POSIX attributes<br>• File permissions<br>• Timestamps<br>• Owner information |
| **Directory Operations** | • Create, delete, move<br>• Directory streams<br>• Walking file trees<br>• Watch service |
| **NIO.2 Features** | • Asynchronous I/O<br>• File system provider<br>• Symbolic links<br>• Better exception handling |

### Code Examples

```java
import java.nio.file.*;
import java.nio.file.attribute.*;
import java.io.IOException;
import java.util.stream.Stream;

// Path Operations
public class PathExamples {
    public static void demonstratePaths() {
        // Creating paths
        Path absolute = Paths.get("/home/user/documents/file.txt");
        Path relative = Paths.get("documents", "file.txt");
        Path current = Paths.get(".");
        Path home = Paths.get(System.getProperty("user.home"));
        
        // Path components
        System.out.println("File name: " + absolute.getFileName());
        System.out.println("Parent: " + absolute.getParent());
        System.out.println("Root: " + absolute.getRoot());
        System.out.println("Name count: " + absolute.getNameCount());
        
        // Path manipulation
        Path normalized = Paths.get("/home/./user/../user/docs").normalize();
        Path resolved = home.resolve("documents/file.txt");
        Path relativized = home.relativize(absolute);
        Path real = absolute.toRealPath();  // Throws IOException
        
        // Subpath
        Path subpath = absolute.subpath(1, 3);  // user/documents
        
        // Conversion
        File file = absolute.toFile();
        Path fromFile = file.toPath();
        URI uri = absolute.toUri();
    }
}

// Files Class Operations
public class FilesOperations {
    public static void demonstrateFiles() throws IOException {
        Path file = Paths.get("example.txt");
        Path dir = Paths.get("example_dir");
        
        // Checking existence and properties
        boolean exists = Files.exists(file);
        boolean notExists = Files.notExists(file);
        boolean isDirectory = Files.isDirectory(dir);
        boolean isRegular = Files.isRegularFile(file);
        boolean isReadable = Files.isReadable(file);
        boolean isWritable = Files.isWritable(file);
        boolean isExecutable = Files.isExecutable(file);
        boolean isHidden = Files.isHidden(file);
        boolean isSame = Files.isSameFile(file, file);
        
        // Creating files and directories
        Path newFile = Files.createFile(Paths.get("new.txt"));
        Path newDir = Files.createDirectory(Paths.get("new_dir"));
        Path newDirs = Files.createDirectories(Paths.get("path/to/dir"));
        Path tempFile = Files.createTempFile("prefix", ".suffix");
        Path tempDir = Files.createTempDirectory("prefix");
        
        // Copying files
        Path target = Paths.get("copy.txt");
        Files.copy(file, target);
        Files.copy(file, target, StandardCopyOption.REPLACE_EXISTING);
        Files.copy(file, target, 
            StandardCopyOption.REPLACE_EXISTING,
            StandardCopyOption.COPY_ATTRIBUTES);
        
        // Moving files
        Files.move(file, target);
        Files.move(file, target, StandardCopyOption.ATOMIC_MOVE);
        
        // Deleting files
        Files.delete(file);  // Throws exception if not exists
        boolean deleted = Files.deleteIfExists(file);  // Returns boolean
        
        // File size
        long size = Files.size(file);
    }
}

// Reading and Writing Files
public class FileReadWriteExamples {
    public static void demonstrateReadWrite() throws IOException {
        Path file = Paths.get("data.txt");
        
        // Reading all content
        byte[] bytes = Files.readAllBytes(file);
        String content = Files.readString(file);  // Java 11+
        List<String> lines = Files.readAllLines(file);
        List<String> linesWithCharset = Files.readAllLines(file, StandardCharsets.UTF_8);
        
        // Writing content
        Files.write(file, "Hello World".getBytes());
        Files.writeString(file, "Hello World");  // Java 11+
        Files.write(file, Arrays.asList("Line 1", "Line 2", "Line 3"));
        Files.write(file, lines, StandardOpenOption.APPEND);
        
        // Using streams for large files
        try (Stream<String> stream = Files.lines(file)) {
            stream.filter(line -> line.contains("important"))
                  .forEach(System.out::println);
        }
        
        // Buffered I/O
        try (BufferedReader reader = Files.newBufferedReader(file)) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        }
        
        try (BufferedWriter writer = Files.newBufferedWriter(file)) {
            writer.write("Line 1");
            writer.newLine();
            writer.write("Line 2");
        }
        
        // Input/Output streams
        try (InputStream is = Files.newInputStream(file);
             OutputStream os = Files.newOutputStream(file)) {
            // Use streams
        }
    }
}

// File Attributes
public class FileAttributeExamples {
    public static void demonstrateAttributes() throws IOException {
        Path file = Paths.get("example.txt");
        
        // Basic attributes
        BasicFileAttributes basic = Files.readAttributes(file, BasicFileAttributes.class);
        System.out.println("Creation time: " + basic.creationTime());
        System.out.println("Last modified: " + basic.lastModifiedTime());
        System.out.println("Last access: " + basic.lastAccessTime());
        System.out.println("Size: " + basic.size());
        System.out.println("Is directory: " + basic.isDirectory());
        System.out.println("Is regular: " + basic.isRegularFile());
        
        // Modifying attributes
        Files.setLastModifiedTime(file, FileTime.fromMillis(System.currentTimeMillis()));
        
        // POSIX attributes (Unix/Linux)
        if (FileSystems.getDefault().supportedFileAttributeViews().contains("posix")) {
            PosixFileAttributes posix = Files.readAttributes(file, PosixFileAttributes.class);
            Set<PosixFilePermission> permissions = posix.permissions();
            UserPrincipal owner = posix.owner();
            GroupPrincipal group = posix.group();
            
            // Set permissions
            Set<PosixFilePermission> perms = PosixFilePermissions.fromString("rw-r--r--");
            Files.setPosixFilePermissions(file, perms);
        }
        
        // DOS attributes (Windows)
        if (FileSystems.getDefault().supportedFileAttributeViews().contains("dos")) {
            DosFileAttributes dos = Files.readAttributes(file, DosFileAttributes.class);
            boolean hidden = dos.isHidden();
            boolean system = dos.isSystem();
            boolean archive = dos.isArchive();
            boolean readOnly = dos.isReadOnly();
            
            // Set attributes
            Files.setAttribute(file, "dos:hidden", true);
        }
        
        // Owner
        UserPrincipal owner = Files.getOwner(file);
        UserPrincipalLookupService lookupService = 
            FileSystems.getDefault().getUserPrincipalLookupService();
        UserPrincipal newOwner = lookupService.lookupPrincipalByName("username");
        Files.setOwner(file, newOwner);
    }
}

// Directory Operations
public class DirectoryOperations {
    public static void demonstrateDirectories() throws IOException {
        Path dir = Paths.get("src");
        
        // List directory contents
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir)) {
            for (Path entry : stream) {
                System.out.println(entry);
            }
        }
        
        // With glob pattern
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir, "*.java")) {
            stream.forEach(System.out::println);
        }
        
        // Using Files.list() (Java 8+)
        try (Stream<Path> stream = Files.list(dir)) {
            stream.filter(Files::isRegularFile)
                  .forEach(System.out::println);
        }
        
        // Walking file tree
        try (Stream<Path> stream = Files.walk(dir)) {
            stream.filter(p -> p.toString().endsWith(".java"))
                  .forEach(System.out::println);
        }
        
        // With depth limit
        try (Stream<Path> stream = Files.walk(dir, 2)) {
            stream.forEach(System.out::println);
        }
        
        // Find files
        try (Stream<Path> stream = Files.find(dir, Integer.MAX_VALUE,
                (path, attrs) -> attrs.isRegularFile() && path.toString().endsWith(".java"))) {
            stream.forEach(System.out::println);
        }
        
        // FileVisitor for complex operations
        Files.walkFileTree(dir, new SimpleFileVisitor<Path>() {
            @Override
            public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) {
                System.out.println("File: " + file);
                return FileVisitResult.CONTINUE;
            }
            
            @Override
            public FileVisitResult preVisitDirectory(Path dir, BasicFileAttributes attrs) {
                System.out.println("Entering: " + dir);
                return FileVisitResult.CONTINUE;
            }
            
            @Override
            public FileVisitResult visitFileFailed(Path file, IOException exc) {
                System.err.println("Failed to visit: " + file);
                return FileVisitResult.SKIP_SUBTREE;
            }
        });
    }
}

// Watch Service
public class WatchServiceExample {
    public static void watchDirectory(Path dir) throws IOException, InterruptedException {
        WatchService watchService = FileSystems.getDefault().newWatchService();
        
        dir.register(watchService, 
            StandardWatchEventKinds.ENTRY_CREATE,
            StandardWatchEventKinds.ENTRY_DELETE,
            StandardWatchEventKinds.ENTRY_MODIFY);
        
        System.out.println("Watching directory: " + dir);
        
        while (true) {
            WatchKey key = watchService.take();  // Blocks until event
            
            for (WatchEvent<?> event : key.pollEvents()) {
                WatchEvent.Kind<?> kind = event.kind();
                
                if (kind == StandardWatchEventKinds.OVERFLOW) {
                    continue;
                }
                
                @SuppressWarnings("unchecked")
                WatchEvent<Path> pathEvent = (WatchEvent<Path>) event;
                Path filename = pathEvent.context();
                
                System.out.println(kind + ": " + filename);
            }
            
            boolean valid = key.reset();
            if (!valid) {
                break;
            }
        }
    }
}
```

### Interview Q&A

**Q1: What advantages does NIO.2 provide over traditional I/O?**
Better exception handling, symbolic link support, file attributes, directory operations, watch service, and asynchronous I/O.

**Q2: What's the difference between Files.delete() and Files.deleteIfExists()?**
delete() throws exception if file doesn't exist, deleteIfExists() returns boolean without exception.

**Q3: How does WatchService work?**
Registers directories for specific events (create, modify, delete), uses OS-level notifications for efficient monitoring.

---

## Chapter 22: Concurrency: Part I

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Thread Basics** | • Unit of execution<br>• Shared memory model<br>• Thread class vs Runnable<br>• Independent call stack |
| **Thread Lifecycle** | • NEW: Created but not started<br>• RUNNABLE: Executing or ready<br>• BLOCKED: Waiting for monitor<br>• WAITING: Waiting indefinitely<br>• TIMED_WAITING: Waiting with timeout<br>• TERMINATED: Completed |
| **Synchronization** | • synchronized keyword<br>• Monitor/lock concept<br>• Intrinsic locks<br>• Reentrant synchronization |
| **Thread Communication** | • wait(), notify(), notifyAll()<br>• Must hold lock<br>• InterruptedException<br>• Spurious wakeups |
| **Thread Issues** | • Race conditions<br>• Deadlock<br>• Livelock<br>• Starvation<br>• Thread safety |

### Code Examples

```java
// Creating Threads
public class ThreadCreation {
    // Method 1: Extending Thread
    static class MyThread extends Thread {
        @Override
        public void run() {
            System.out.println("Thread: " + Thread.currentThread().getName());
        }
    }
    
    // Method 2: Implementing Runnable
    static class MyRunnable implements Runnable {
        @Override
        public void run() {
            System.out.println("Runnable: " + Thread.currentThread().getName());
        }
    }
    
    public static void demonstrateCreation() {
        // Using Thread class
        MyThread thread1 = new MyThread();
        thread1.start();  // Don't call run() directly!
        
        // Using Runnable
        Thread thread2 = new Thread(new MyRunnable());
        thread2.start();
        
        // Using lambda (Runnable is functional interface)
        Thread thread3 = new Thread(() -> {
            System.out.println("Lambda: " + Thread.currentThread().getName());
        });
        thread3.start();
        
        // Thread with name and priority
        Thread thread4 = new Thread(() -> {
            System.out.println("Custom thread running");
        }, "CustomThread");
        thread4.setPriority(Thread.MAX_PRIORITY);
        thread4.start();
    }
}

// Thread Lifecycle and States
public class ThreadLifecycle {
    public static void demonstrateStates() throws InterruptedException {
        Thread thread = new Thread(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        
        System.out.println("State after creation: " + thread.getState()); // NEW
        
        thread.start();
        System.out.println("State after start: " + thread.getState()); // RUNNABLE
        
        Thread.sleep(100);
        System.out.println("State while sleeping: " + thread.getState()); // TIMED_WAITING
        
        thread.join();
        System.out.println("State after completion: " + thread.getState()); // TERMINATED
    }
    
    // Thread methods
    public static void demonstrateMethods() throws InterruptedException {
        Thread current = Thread.currentThread();
        System.out.println("Current thread: " + current.getName());
        System.out.println("Thread ID: " + current.getId());
        System.out.println("Priority: " + current.getPriority());
        System.out.println("Is daemon: " + current.isDaemon());
        System.out.println("Is alive: " + current.isAlive());
        
        // Join - wait for thread to complete
        Thread worker = new Thread(() -> {
            try {
                Thread.sleep(2000);
                System.out.println("Worker done");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
        worker.start();
        worker.join();  // Main thread waits for worker
        System.out.println("Main continues after worker");
        
        // Daemon threads
        Thread daemon = new Thread(() -> {
            while (true) {
                System.out.println("Daemon working...");
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    break;
                }
            }
        });
        daemon.setDaemon(true);  // Must set before start
        daemon.start();
    }
}

// Synchronization
public class SynchronizationExamples {
    private int counter = 0;
    private final Object lock = new Object();
    
    // Synchronized method
    public synchronized void incrementSync() {
        counter++;
    }
    
    // Synchronized block
    public void incrementBlock() {
        synchronized (lock) {
            counter++;
        }
    }
    
    // Static synchronization
    private static int staticCounter = 0;
    
    public static synchronized void staticIncrement() {
        staticCounter++;
    }
    
    // Equivalent to above
    public static void staticIncrementBlock() {
        synchronized (SynchronizationExamples.class) {
            staticCounter++;
        }
    }
    
    // Bank account example
    static class BankAccount {
        private double balance;
        
        public synchronized void deposit(double amount) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        }
        
        public synchronized void withdraw(double amount) {
            if (balance >= amount) {
                balance -= amount;
                System.out.println("Withdrawn: " + amount);
            } else {
                System.out.println("Insufficient funds");
            }
        }
        
        public synchronized double getBalance() {
            return balance;
        }
        
        // Transfer between accounts
        public static void transfer(BankAccount from, BankAccount to, double amount) {
            // Avoid deadlock by ordering locks
            BankAccount first = from.hashCode() < to.hashCode() ? from : to;
            BankAccount second = from.hashCode() < to.hashCode() ? to : from;
            
            synchronized (first) {
                synchronized (second) {
                    from.withdraw(amount);
                    to.deposit(amount);
                }
            }
        }
    }
}

// Wait and Notify
public class WaitNotifyExamples {
    static class SharedResource {
        private boolean available = false;
        private String data;
        
        public synchronized void produce(String newData) {
            while (available) {
                try {
                    wait();  // Release lock and wait
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    return;
                }
            }
            data = newData;
            available = true;
            notify();  // Wake up one waiting thread
        }
        
        public synchronized String consume() {
            while (!available) {
                try {
                    wait();
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    return null;
                }
            }
            available = false;
            notify();
            return data;
        }
    }
    
    // Bounded buffer example
    static class BoundedBuffer<T> {
        private final Queue<T> queue = new LinkedList<>();
        private final int capacity;
        
        public BoundedBuffer(int capacity) {
            this.capacity = capacity;
        }
        
        public synchronized void put(T item) throws InterruptedException {
            while (queue.size() == capacity) {
                wait();
            }
            queue.offer(item);
            notifyAll();  // Wake all waiting threads
        }
        
        public synchronized T take() throws InterruptedException {
            while (queue.isEmpty()) {
                wait();
            }
            T item = queue.poll();
            notifyAll();
            return item;
        }
    }
}

// Common Concurrency Problems
public class ConcurrencyProblems {
    // Race condition example
    static class Counter {
        private int count = 0;
        
        // NOT thread-safe
        public void increment() {
            count++;  // Read-modify-write not atomic
        }
        
        // Thread-safe version
        public synchronized void safeIncrement() {
            count++;
        }
    }
    
    // Deadlock example
    public static void demonstrateDeadlock() {
        final Object lock1 = new Object();
        final Object lock2 = new Object();
        
        Thread t1 = new Thread(() -> {
            synchronized (lock1) {
                System.out.println("Thread 1: Holding lock 1");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                System.out.println("Thread 1: Waiting for lock 2");
                synchronized (lock2) {
                    System.out.println("Thread 1: Acquired lock 2");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized (lock2) {
                System.out.println("Thread 2: Holding lock 2");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                System.out.println("Thread 2: Waiting for lock 1");
                synchronized (lock1) {
                    System.out.println("Thread 2: Acquired lock 1");
                }
            }
        });
        
        t1.start();
        t2.start();
        // Results in deadlock!
    }
    
    // Livelock example (threads actively responding but making no progress)
    static class Polite {
        private boolean passingCorridor = false;
        
        public synchronized void pass(Polite other) {
            while (other.isPassingCorridor()) {
                try {
                    wait();
                } catch (InterruptedException e) {}
            }
            passingCorridor = true;
            // Pass corridor
            passingCorridor = false;
            notifyAll();
        }
        
        public synchronized boolean isPassingCorridor() {
            return passingCorridor;
        }
    }
}
```

### Interview Q&A

**Q1: What's the difference between wait() and sleep()?**
- wait(): Releases lock, must be in synchronized context, woken by notify()
- sleep(): Doesn't release lock, can be called anywhere, woken by timeout or interrupt

**Q2: How do you prevent deadlock?**
- Order lock acquisition consistently
- Use timeouts (tryLock)
- Avoid nested locks
- Use java.util.concurrent utilities

**Q3: What's the difference between synchronized method and synchronized block?**
- Method: Locks entire method, uses 'this' or class object
- Block: More granular control, can specify lock object, better performance

---

## Chapter 23: Concurrency: Part II

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Executor Framework** | • Thread pool management<br>• ExecutorService interface<br>• Scheduled execution<br>• Future and Callable |
| **Fork/Join Framework** | • Work-stealing algorithm<br>• RecursiveTask/RecursiveAction<br>• Parallel divide-and-conquer<br>• ForkJoinPool |
| **Concurrent Collections** | • Thread-safe collections<br>• ConcurrentHashMap<br>• CopyOnWriteArrayList<br>• BlockingQueue implementations |
| **Synchronizers** | • CountDownLatch<br>• CyclicBarrier<br>• Semaphore<br>• Phaser<br>• Exchanger |
| **Atomic Variables** | • Lock-free thread-safe operations<br>• AtomicInteger, AtomicLong<br>• AtomicReference<br>• Compare-and-swap |

### Code Examples

```java
import java.util.concurrent.*;
import java.util.concurrent.atomic.*;

// Executor Framework
public class ExecutorExamples {
    public static void demonstrateExecutors() throws Exception {
        // Fixed thread pool
        ExecutorService fixedPool = Executors.newFixedThreadPool(4);
        
        // Cached thread pool (creates threads as needed)
        ExecutorService cachedPool = Executors.newCachedThreadPool();
        
        // Single thread executor
        ExecutorService singleThread = Executors.newSingleThreadExecutor();
        
        // Scheduled executor
        ScheduledExecutorService scheduled = Executors.newScheduledThreadPool(2);
        
        // Submit tasks
        fixedPool.execute(() -> System.out.println("Runnable task"));
        
        // Callable with Future
        Future<Integer> future = fixedPool.submit(() -> {
            Thread.sleep(1000);
            return 42;
        });
        
        // Get result (blocks until complete)
        Integer result = future.get();
        Integer resultWithTimeout = future.get(5, TimeUnit.SECONDS);
        
        // Check status
        boolean done = future.isDone();
        boolean cancelled = future.isCancelled();
        future.cancel(true);  // Interrupt if running
        
        // Scheduled execution
        scheduled.schedule(() -> System.out.println("Delayed"), 5, TimeUnit.SECONDS);
        
        scheduled.scheduleAtFixedRate(
            () -> System.out.println("Fixed rate"),
            0, 2, TimeUnit.SECONDS
        );
        
        scheduled.scheduleWithFixedDelay(
            () -> System.out.println("Fixed delay"),
            0, 2, TimeUnit.SECONDS
        );
        
        // Shutdown
        fixedPool.shutdown();  // No new tasks
        fixedPool.awaitTermination(60, TimeUnit.SECONDS);
        
        // Force shutdown
        List<Runnable> pending = fixedPool.shutdownNow();
    }
    
    // CompletableFuture
    public static void demonstrateCompletableFuture() {
        // Creating
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {}
            return "Result";
        });
        
        // Chaining
        CompletableFuture<Integer> chain = future
            .thenApply(s -> s.length())
            .thenApply(len -> len * 2)
            .exceptionally(ex -> 0);
        
        // Combining futures
        CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> "Hello");
        CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> "World");
        
        CompletableFuture<String> combined = future1
            .thenCombine(future2, (s1, s2) -> s1 + " " + s2);
        
        // Multiple futures
        CompletableFuture<Void> allOf = CompletableFuture.allOf(future1, future2);
        CompletableFuture<Object> anyOf = CompletableFuture.anyOf(future1, future2);
    }
}

// Fork/Join Framework
public class ForkJoinExamples {
    // RecursiveTask returns a result
    static class FibonacciTask extends RecursiveTask<Long> {
        private final long n;
        
        FibonacciTask(long n) {
            this.n = n;
        }
        
        @Override
        protected Long compute() {
            if (n <= 1) return n;
            
            FibonacciTask f1 = new FibonacciTask(n - 1);
            FibonacciTask f2 = new FibonacciTask(n - 2);
            
            f1.fork();  // Execute async
            long result2 = f2.compute();  // Execute in current thread
            long result1 = f1.join();  // Wait for result
            
            return result1 + result2;
        }
    }
    
    // RecursiveAction doesn't return a result
    static class MergeSortAction extends RecursiveAction {
        private int[] array;
        private int start, end;
        
        MergeSortAction(int[] array, int start, int end) {
            this.array = array;
            this.start = start;
            this.end = end;
        }
        
        @Override
        protected void compute() {
            if (end - start <= 1) return;
            
            int mid = (start + end) / 2;
            
            MergeSortAction left = new MergeSortAction(array, start, mid);
            MergeSortAction right = new MergeSortAction(array, mid, end);
            
            invokeAll(left, right);  // Fork and join both
            
            merge(array, start, mid, end);
        }
        
        private void merge(int[] array, int start, int mid, int end) {
            // Merge implementation
        }
    }
    
    public static void demonstrateForkJoin() {
        ForkJoinPool pool = new ForkJoinPool();
        // Or use common pool: ForkJoinPool.commonPool()
        
        FibonacciTask task = new FibonacciTask(20);
        Long result = pool.invoke(task);
        
        // Parallel arrays operation
        int[] array = new int[1000000];
        Arrays.parallelSort(array);
        Arrays.parallelPrefix(array, (x, y) -> x + y);
        Arrays.parallelSetAll(array, i -> i * 2);
    }
}

// Concurrent Collections
public class ConcurrentCollectionExamples {
    public static void demonstrateConcurrentCollections() {
        // ConcurrentHashMap
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
        map.put("key", 1);
        map.compute("key", (k, v) -> v == null ? 1 : v + 1);
        map.merge("key", 1, Integer::sum);
        
        // Parallel operations
        map.forEach(1, (k, v) -> System.out.println(k + "=" + v));
        
        // CopyOnWriteArrayList - good for many reads, few writes
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        list.add("item");
        
        // BlockingQueue implementations
        BlockingQueue<String> arrayQueue = new ArrayBlockingQueue<>(10);
        BlockingQueue<String> linkedQueue = new LinkedBlockingQueue<>();
        BlockingQueue<String> priorityQueue = new PriorityBlockingQueue<>();
        BlockingQueue<String> delayQueue = new DelayQueue<>();
        BlockingQueue<String> synchronousQueue = new SynchronousQueue<>();
        
        // Producer-Consumer with BlockingQueue
        class Producer implements Runnable {
            private BlockingQueue<String> queue;
            
            Producer(BlockingQueue<String> queue) {
                this.queue = queue;
            }
            
            public void run() {
                try {
                    queue.put("item");  // Blocks if full
                    queue.offer("item", 1, TimeUnit.SECONDS);  // Timeout
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        }
        
        class Consumer implements Runnable {
            private BlockingQueue<String> queue;
            
            Consumer(BlockingQueue<String> queue) {
                this.queue = queue;
            }
            
            public void run() {
                try {
                    String item = queue.take();  // Blocks if empty
                    String item2 = queue.poll(1, TimeUnit.SECONDS);  // Timeout
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        }
    }
}

// Synchronizers
public class SynchronizerExamples {
    // CountDownLatch - one-time event
    public static void demonstrateCountDownLatch() throws InterruptedException {
        int workerCount = 3;
        CountDownLatch startSignal = new CountDownLatch(1);
        CountDownLatch doneSignal = new CountDownLatch(workerCount);
        
        for (int i = 0; i < workerCount; i++) {
            new Thread(() -> {
                try {
                    startSignal.await();  // Wait for start signal
                    System.out.println("Worker started");
                    Thread.sleep(1000);
                    doneSignal.countDown();  // Signal completion
                } catch (InterruptedException e) {}
            }).start();
        }
        
        System.out.println("Starting workers...");
        startSignal.countDown();  // Release all workers
        doneSignal.await();  // Wait for all to complete
        System.out.println("All workers done");
    }
    
    // CyclicBarrier - reusable synchronization point
    public static void demonstrateCyclicBarrier() {
        int parties = 3;
        CyclicBarrier barrier = new CyclicBarrier(parties, () -> {
            System.out.println("All parties arrived, barrier action executed");
        });
        
        for (int i = 0; i < parties; i++) {
            new Thread(() -> {
                try {
                    System.out.println("Thread waiting at barrier");
                    barrier.await();
                    System.out.println("Thread passed barrier");
                    
                    // Reuse barrier
                    Thread.sleep(1000);
                    barrier.await();  // Can use again
                } catch (Exception e) {}
            }).start();
        }
    }
    
    // Semaphore - resource pool
    public static void demonstrateSemaphore() {
        Semaphore semaphore = new Semaphore(3);  // 3 permits
        
        for (int i = 0; i < 10; i++) {
            new Thread(() -> {
                try {
                    semaphore.acquire();  // Get permit
                    System.out.println("Acquired permit");
                    Thread.sleep(1000);
                    semaphore.release();  // Release permit
                } catch (InterruptedException e) {}
            }).start();
        }
    }
    
    // Phaser - dynamic parties
    public static void demonstratePhaser() {
        Phaser phaser = new Phaser(1);  // Register self
        
        for (int i = 0; i < 3; i++) {
            phaser.register();  // Register new party
            new Thread(() -> {
                System.out.println("Phase " + phaser.getPhase());
                phaser.arriveAndAwaitAdvance();
                
                System.out.println("Phase " + phaser.getPhase());
                phaser.arriveAndDeregister();
            }).start();
        }
        
        phaser.arriveAndDeregister();  // Deregister self
    }
}

// Atomic Variables
public class AtomicExamples {
    private AtomicInteger counter = new AtomicInteger(0);
    private AtomicLong longCounter = new AtomicLong(0);
    private AtomicBoolean flag = new AtomicBoolean(false);
    private AtomicReference<String> reference = new AtomicReference<>("initial");
    
    public void demonstrateAtomic() {
        // Basic operations
        int value = counter.get();
        counter.set(10);
        int oldValue = counter.getAndSet(20);
        
        // Atomic arithmetic
        counter.incrementAndGet();  // ++counter
        counter.getAndIncrement();  // counter++
        counter.decrementAndGet();  // --counter
        counter.getAndDecrement();  // counter--
        counter.addAndGet(5);
        counter.getAndAdd(5);
        
        // Compare and swap
        boolean success = counter.compareAndSet(20, 30);
        
        // Update operations
        counter.updateAndGet(x -> x * 2);
        counter.getAndUpdate(x -> x + 10);
        
        // Accumulate
        counter.accumulateAndGet(5, (x, y) -> x + y);
        
        // AtomicReference
        String old = reference.getAndSet("new");
        reference.compareAndSet("new", "newer");
        reference.updateAndGet(s -> s.toUpperCase());
    }
}
```

### Interview Q&A

**Q1: When would you use ConcurrentHashMap vs Collections.synchronizedMap()?**
ConcurrentHashMap offers better performance with segment-based locking and doesn't lock for reads. synchronizedMap locks entire map for all operations.

**Q2: What's the difference between execute() and submit() in ExecutorService?**
- execute(): void return, for Runnable only
- submit(): Returns Future, accepts Callable or Runnable

**Q3: When should you use Fork/Join vs ExecutorService?**
Fork/Join for recursive divide-and-conquer with work-stealing. ExecutorService for independent tasks without recursive decomposition.

---
## Chapter 24: Database Connectivity

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Relational Databases** | • Tables with rows and columns<br>• Primary keys for unique identification<br>• Foreign keys for relationships<br>• SQL for data manipulation<br>• ACID properties (Atomicity, Consistency, Isolation, Durability) |
| **JDBC Architecture** | • Driver Manager: Manages drivers<br>• Connection: Database session<br>• Statement: SQL execution<br>• ResultSet: Query results<br>• SQLException: Error handling |
| **JDBC Drivers** | • Type 1: JDBC-ODBC bridge (deprecated)<br>• Type 2: Native API<br>• Type 3: Network protocol<br>• Type 4: Pure Java (most common) |
| **Connection Management** | • DriverManager.getConnection()<br>• Connection URL format<br>• Connection pooling<br>• Try-with-resources for cleanup |
| **Statement Types** | • Statement: Simple SQL<br>• PreparedStatement: Parameterized, precompiled<br>• CallableStatement: Stored procedures |
| **ResultSet** | • Forward-only by default<br>• Scrollable types<br>• Updatable ResultSets<br>• ResultSetMetaData |
| **Transactions** | • Auto-commit mode<br>• Manual transaction control<br>• Commit and rollback<br>• Savepoints<br>• Isolation levels |
| **Batch Processing** | • Execute multiple statements<br>• Better performance<br>• addBatch() and executeBatch() |

### Code Examples

```java
import java.sql.*;
import javax.sql.DataSource;
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

// Basic JDBC Connection and Query
public class JDBCBasics {
    private static final String URL = "jdbc:mysql://localhost:3306/testdb";
    private static final String USER = "username";
    private static final String PASSWORD = "password";
    
    public static void demonstrateBasicJDBC() {
        // Basic connection and query
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT * FROM users")) {
            
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                String email = rs.getString("email");
                Date created = rs.getDate("created_date");
                
                System.out.printf("ID: %d, Name: %s, Email: %s, Created: %s%n",
                    id, name, email, created);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    // Connection with properties
    public static Connection getConnection() throws SQLException {
        Properties props = new Properties();
        props.setProperty("user", USER);
        props.setProperty("password", PASSWORD);
        props.setProperty("ssl", "true");
        
        return DriverManager.getConnection(URL, props);
    }
}

// PreparedStatement Examples
public class PreparedStatementExamples {
    // Insert with PreparedStatement
    public static void insertUser(Connection conn, String name, String email, int age) 
            throws SQLException {
        String sql = "INSERT INTO users (name, email, age) VALUES (?, ?, ?)";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql, 
                Statement.RETURN_GENERATED_KEYS)) {
            pstmt.setString(1, name);
            pstmt.setString(2, email);
            pstmt.setInt(3, age);
            
            int rowsAffected = pstmt.executeUpdate();
            
            // Get generated key
            if (rowsAffected > 0) {
                try (ResultSet generatedKeys = pstmt.getGeneratedKeys()) {
                    if (generatedKeys.next()) {
                        long id = generatedKeys.getLong(1);
                        System.out.println("Generated ID: " + id);
                    }
                }
            }
        }
    }
    
    // Update with PreparedStatement
    public static void updateUser(Connection conn, long id, String newEmail) 
            throws SQLException {
        String sql = "UPDATE users SET email = ? WHERE id = ?";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, newEmail);
            pstmt.setLong(2, id);
            
            int rowsUpdated = pstmt.executeUpdate();
            System.out.println("Rows updated: " + rowsUpdated);
        }
    }
    
    // Delete with PreparedStatement
    public static void deleteUser(Connection conn, long id) throws SQLException {
        String sql = "DELETE FROM users WHERE id = ?";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setLong(1, id);
            
            int rowsDeleted = pstmt.executeUpdate();
            System.out.println("Rows deleted: " + rowsDeleted);
        }
    }
    
    // Batch operations
    public static void batchInsert(Connection conn, List<User> users) 
            throws SQLException {
        String sql = "INSERT INTO users (name, email, age) VALUES (?, ?, ?)";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            for (User user : users) {
                pstmt.setString(1, user.getName());
                pstmt.setString(2, user.getEmail());
                pstmt.setInt(3, user.getAge());
                pstmt.addBatch();
            }
            
            int[] results = pstmt.executeBatch();
            System.out.println("Batch insert completed: " + results.length + " records");
        }
    }
}

// ResultSet Navigation and Updates
public class ResultSetExamples {
    public static void demonstrateScrollableResultSet(Connection conn) 
            throws SQLException {
        // Create scrollable, updatable ResultSet
        String sql = "SELECT * FROM users";
        try (Statement stmt = conn.createStatement(
                ResultSet.TYPE_SCROLL_INSENSITIVE,
                ResultSet.CONCUR_UPDATABLE);
             ResultSet rs = stmt.executeQuery(sql)) {
            
            // Navigate ResultSet
            rs.last();  // Move to last row
            System.out.println("Total rows: " + rs.getRow());
            
            rs.first();  // Move to first row
            System.out.println("First user: " + rs.getString("name"));
            
            rs.absolute(5);  // Move to 5th row
            rs.relative(-2);  // Move back 2 rows
            
            // Update through ResultSet
            rs.updateString("email", "newemail@example.com");
            rs.updateRow();  // Apply update to database
            
            // Insert through ResultSet
            rs.moveToInsertRow();
            rs.updateString("name", "New User");
            rs.updateString("email", "newuser@example.com");
            rs.updateInt("age", 25);
            rs.insertRow();
            rs.moveToCurrentRow();
        }
    }
    
    // ResultSet metadata
    public static void printMetadata(ResultSet rs) throws SQLException {
        ResultSetMetaData metaData = rs.getMetaData();
        int columnCount = metaData.getColumnCount();
        
        for (int i = 1; i <= columnCount; i++) {
            System.out.println("Column " + i + ":");
            System.out.println("  Name: " + metaData.getColumnName(i));
            System.out.println("  Type: " + metaData.getColumnTypeName(i));
            System.out.println("  Size: " + metaData.getColumnDisplaySize(i));
            System.out.println("  Nullable: " + metaData.isNullable(i));
        }
    }
}

// Transaction Management
public class TransactionExamples {
    public static void transferMoney(Connection conn, long fromAccount, 
            long toAccount, double amount) throws SQLException {
        
        // Disable auto-commit for transaction
        conn.setAutoCommit(false);
        
        try {
            // Debit from account
            String debitSql = "UPDATE accounts SET balance = balance - ? WHERE id = ?";
            try (PreparedStatement pstmt = conn.prepareStatement(debitSql)) {
                pstmt.setDouble(1, amount);
                pstmt.setLong(2, fromAccount);
                pstmt.executeUpdate();
            }
            
            // Check balance
            String checkSql = "SELECT balance FROM accounts WHERE id = ?";
            try (PreparedStatement pstmt = conn.prepareStatement(checkSql)) {
                pstmt.setLong(1, fromAccount);
                try (ResultSet rs = pstmt.executeQuery()) {
                    if (rs.next() && rs.getDouble("balance") < 0) {
                        throw new SQLException("Insufficient funds");
                    }
                }
            }
            
            // Credit to account
            String creditSql = "UPDATE accounts SET balance = balance + ? WHERE id = ?";
            try (PreparedStatement pstmt = conn.prepareStatement(creditSql)) {
                pstmt.setDouble(1, amount);
                pstmt.setLong(2, toAccount);
                pstmt.executeUpdate();
            }
            
            // Commit transaction
            conn.commit();
            System.out.println("Transfer successful");
            
        } catch (SQLException e) {
            // Rollback on error
            conn.rollback();
            System.err.println("Transfer failed: " + e.getMessage());
            throw e;
        } finally {
            conn.setAutoCommit(true);
        }
    }
    
    // Savepoints
    public static void demonstrateSavepoints(Connection conn) throws SQLException {
        conn.setAutoCommit(false);
        Savepoint savepoint1 = null;
        Savepoint savepoint2 = null;
        
        try {
            // First operation
            executeUpdate(conn, "INSERT INTO log (message) VALUES ('Step 1')");
            savepoint1 = conn.setSavepoint("SP1");
            
            // Second operation
            executeUpdate(conn, "INSERT INTO log (message) VALUES ('Step 2')");
            savepoint2 = conn.setSavepoint("SP2");
            
            // Third operation (might fail)
            executeUpdate(conn, "INSERT INTO log (message) VALUES ('Step 3')");
            
            conn.commit();
        } catch (SQLException e) {
            if (savepoint2 != null) {
                conn.rollback(savepoint2);  // Rollback to savepoint 2
                conn.commit();  // Commit up to savepoint 2
            } else if (savepoint1 != null) {
                conn.rollback(savepoint1);  // Rollback to savepoint 1
                conn.commit();  // Commit up to savepoint 1
            } else {
                conn.rollback();  // Full rollback
            }
        } finally {
            conn.setAutoCommit(true);
        }
    }
    
    private static void executeUpdate(Connection conn, String sql) 
            throws SQLException {
        try (Statement stmt = conn.createStatement()) {
            stmt.executeUpdate(sql);
        }
    }
}

// CallableStatement for Stored Procedures
public class StoredProcedureExamples {
    public static void callStoredProcedure(Connection conn) throws SQLException {
        // Call stored procedure with IN and OUT parameters
        String sql = "{call getUserDetails(?, ?, ?)}";
        
        try (CallableStatement cstmt = conn.prepareCall(sql)) {
            // Set IN parameter
            cstmt.setLong(1, 123);  // User ID
            
            // Register OUT parameters
            cstmt.registerOutParameter(2, Types.VARCHAR);  // Name
            cstmt.registerOutParameter(3, Types.VARCHAR);  // Email
            
            // Execute
            cstmt.execute();
            
            // Get OUT parameters
            String name = cstmt.getString(2);
            String email = cstmt.getString(3);
            
            System.out.println("Name: " + name + ", Email: " + email);
        }
    }
    
    // Function call
    public static void callFunction(Connection conn) throws SQLException {
        String sql = "{? = call calculateDiscount(?, ?)}";
        
        try (CallableStatement cstmt = conn.prepareCall(sql)) {
            // Register return value
            cstmt.registerOutParameter(1, Types.DOUBLE);
            
            // Set parameters
            cstmt.setDouble(2, 100.00);  // Price
            cstmt.setInt(3, 10);  // Discount percentage
            
            cstmt.execute();
            
            double discountedPrice = cstmt.getDouble(1);
            System.out.println("Discounted price: " + discountedPrice);
        }
    }
}

// Connection Pooling with HikariCP
public class ConnectionPoolExample {
    private static HikariDataSource dataSource;
    
    static {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://localhost:3306/testdb");
        config.setUsername("username");
        config.setPassword("password");
        config.setMaximumPoolSize(10);
        config.setMinimumIdle(5);
        config.setConnectionTimeout(30000);
        config.setIdleTimeout(600000);
        config.setMaxLifetime(1800000);
        
        dataSource = new HikariDataSource(config);
    }
    
    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection();
    }
    
    public static void closeDataSource() {
        if (dataSource != null) {
            dataSource.close();
        }
    }
}

// Database Metadata
public class DatabaseMetadataExample {
    public static void exploreDatabaseMetadata(Connection conn) throws SQLException {
        DatabaseMetaData metaData = conn.getMetaData();
        
        // Database info
        System.out.println("Database: " + metaData.getDatabaseProductName());
        System.out.println("Version: " + metaData.getDatabaseProductVersion());
        System.out.println("Driver: " + metaData.getDriverName());
        
        // List tables
        try (ResultSet tables = metaData.getTables(null, null, "%", 
                new String[]{"TABLE"})) {
            while (tables.next()) {
                String tableName = tables.getString("TABLE_NAME");
                System.out.println("Table: " + tableName);
                
                // List columns for each table
                try (ResultSet columns = metaData.getColumns(null, null, 
                        tableName, null)) {
                    while (columns.next()) {
                        System.out.println("  Column: " + 
                            columns.getString("COLUMN_NAME") + 
                            " (" + columns.getString("TYPE_NAME") + ")");
                    }
                }
            }
        }
    }
}

// Helper class
class User {
    private String name;
    private String email;
    private int age;
    
    // Constructor and getters
    public User(String name, String email, int age) {
        this.name = name;
        this.email = email;
        this.age = age;
    }
    
    public String getName() { return name; }
    public String getEmail() { return email; }
    public int getAge() { return age; }
}
```

### Interview Q&A

**Q1: What's the difference between Statement and PreparedStatement?**
- **Statement**: Simple SQL execution, vulnerable to SQL injection, parsed each time
- **PreparedStatement**: Precompiled, prevents SQL injection through parameterization, better performance for repeated execution

**Q2: How do you prevent SQL injection?**
- Use PreparedStatement with parameterized queries
- Never concatenate user input into SQL strings
- Validate and sanitize input
- Use stored procedures where appropriate
- Apply principle of least privilege to database users

**Q3: Explain transaction isolation levels.**
- **READ_UNCOMMITTED**: Can read uncommitted changes (dirty reads)
- **READ_COMMITTED**: Only reads committed data
- **REPEATABLE_READ**: Prevents dirty and non-repeatable reads
- **SERIALIZABLE**: Highest isolation, prevents all phenomena

**Q4: What is connection pooling and why use it?**
Connection pooling maintains a cache of database connections that can be reused, avoiding the overhead of creating new connections. Benefits include improved performance, resource management, and scalability.

---

## Chapter 25: Annotations

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Annotation Basics** | • Metadata for code<br>• @ symbol prefix<br>• Compile-time and runtime processing<br>• No direct effect on code operation<br>• Can be processed by tools |
| **Built-in Annotations** | • @Override: Method overriding<br>• @Deprecated: Mark as obsolete<br>• @SuppressWarnings: Suppress compiler warnings<br>• @FunctionalInterface: Single abstract method<br>• @SafeVarargs: Varargs type safety |
| **Meta-Annotations** | • @Target: Where annotation can be used<br>• @Retention: How long annotation retained<br>• @Documented: Include in Javadoc<br>• @Inherited: Inherited by subclasses<br>• @Repeatable: Can be applied multiple times |
| **Custom Annotations** | • Define with @interface<br>• Element types limited<br>• Default values supported<br>• No null values<br>• Can include other annotations |
| **Retention Policies** | • SOURCE: Discarded by compiler<br>• CLASS: In bytecode, not at runtime<br>• RUNTIME: Available via reflection |
| **Element Types** | • TYPE: Class, interface, enum<br>• FIELD: Field declaration<br>• METHOD: Method declaration<br>• PARAMETER: Method parameter<br>• CONSTRUCTOR: Constructor<br>• LOCAL_VARIABLE: Local variable<br>• ANNOTATION_TYPE: Annotation type<br>• PACKAGE: Package declaration |
| **Processing** | • Compile-time: Annotation processors<br>• Runtime: Reflection API<br>• Generate code, validate, configure |

### Code Examples

```java
import java.lang.annotation.*;
import java.lang.reflect.*;
import javax.annotation.processing.*;

// Built-in Annotations Usage
public class BuiltInAnnotations {
    
    @Deprecated(since = "1.5", forRemoval = true)
    public void oldMethod() {
        System.out.println("This method is deprecated");
    }
    
    @Override
    public String toString() {
        return "BuiltInAnnotations instance";
    }
    
    @SuppressWarnings({"unchecked", "rawtypes"})
    public void useRawTypes() {
        List list = new ArrayList();
        list.add("String");
    }
    
    @SafeVarargs
    public final <T> void safeVarargsMethod(T... values) {
        for (T value : values) {
            System.out.println(value);
        }
    }
}

// Custom Annotation Definitions
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Documented
public @interface Entity {
    String tableName() default "";
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface Column {
    String name() default "";
    boolean nullable() default true;
    int length() default 255;
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface Id {
    boolean autoGenerate() default true;
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Transactional {
    enum IsolationLevel {
        READ_UNCOMMITTED, READ_COMMITTED, 
        REPEATABLE_READ, SERIALIZABLE
    }
    
    IsolationLevel isolation() default IsolationLevel.READ_COMMITTED;
    boolean readOnly() default false;
    int timeout() default -1;
    Class<? extends Exception>[] rollbackFor() default {};
}

// Using Custom Annotations
@Entity(tableName = "users")
public class User {
    @Id
    @Column(name = "user_id", nullable = false)
    private Long id;
    
    @Column(name = "username", nullable = false, length = 50)
    private String username;
    
    @Column(name = "email", nullable = false, length = 100)
    private String email;
    
    @Column(name = "created_date")
    private LocalDateTime createdDate;
    
    @Transactional(
        isolation = Transactional.IsolationLevel.REPEATABLE_READ,
        timeout = 30,
        rollbackFor = {SQLException.class, DataAccessException.class}
    )
    public void save() {
        // Save logic
    }
}

// Repeatable Annotations
@Repeatable(Schedules.class)
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Schedule {
    String cron();
    String timezone() default "UTC";
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Schedules {
    Schedule[] value();
}

// Using Repeatable Annotations
public class ScheduledTask {
    @Schedule(cron = "0 0 * * * *", timezone = "EST")
    @Schedule(cron = "0 30 * * * *", timezone = "PST")
    public void runTask() {
        System.out.println("Task executed");
    }
}

// Processing Annotations at Runtime
public class AnnotationProcessor {
    public static void processEntity(Class<?> clazz) {
        // Process class-level annotations
        if (clazz.isAnnotationPresent(Entity.class)) {
            Entity entity = clazz.getAnnotation(Entity.class);
            String tableName = entity.tableName().isEmpty() ? 
                clazz.getSimpleName().toLowerCase() : entity.tableName();
            System.out.println("Table: " + tableName);
            
            // Process field annotations
            for (Field field : clazz.getDeclaredFields()) {
                if (field.isAnnotationPresent(Column.class)) {
                    Column column = field.getAnnotation(Column.class);
                    String columnName = column.name().isEmpty() ? 
                        field.getName() : column.name();
                    
                    System.out.printf("Column: %s, Nullable: %b, Length: %d%n",
                        columnName, column.nullable(), column.length());
                    
                    if (field.isAnnotationPresent(Id.class)) {
                        Id id = field.getAnnotation(Id.class);
                        System.out.println("  Primary Key, Auto-generate: " + 
                            id.autoGenerate());
                    }
                }
            }
            
            // Process method annotations
            for (Method method : clazz.getDeclaredMethods()) {
                if (method.isAnnotationPresent(Transactional.class)) {
                    Transactional tx = method.getAnnotation(Transactional.class);
                    System.out.printf("Method %s: Isolation=%s, ReadOnly=%b%n",
                        method.getName(), tx.isolation(), tx.readOnly());
                }
            }
        }
    }
    
    public static void main(String[] args) {
        processEntity(User.class);
    }
}

// Compile-time Annotation Processor
@SupportedAnnotationTypes("com.example.GenerateBuilder")
@SupportedSourceVersion(SourceVersion.RELEASE_17)
public class BuilderProcessor extends AbstractProcessor {
    
    @Override
    public boolean process(Set<? extends TypeElement> annotations, 
                          RoundEnvironment roundEnv) {
        for (Element element : roundEnv.getElementsAnnotatedWith(GenerateBuilder.class)) {
            if (element.getKind() == ElementKind.CLASS) {
                generateBuilderClass((TypeElement) element);
            }
        }
        return true;
    }
    
    private void generateBuilderClass(TypeElement classElement) {
        String className = classElement.getSimpleName().toString();
        String builderClassName = className + "Builder";
        
        // Generate builder class code
        // This would typically use JavaPoet or similar library
        System.out.println("Generating " + builderClassName);
    }
}

// Validation Annotations
@Target({ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
public @interface NotNull {
    String message() default "Value cannot be null";
}

@Target({ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
public @interface Size {
    int min() default 0;
    int max() default Integer.MAX_VALUE;
    String message() default "Size must be between {min} and {max}";
}

@Target({ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
public @interface Pattern {
    String regexp();
    String message() default "Must match pattern {regexp}";
}

// Using Validation Annotations
public class ValidationExample {
    @NotNull(message = "Name is required")
    @Size(min = 2, max = 50, message = "Name must be between 2 and 50 characters")
    private String name;
    
    @NotNull
    @Pattern(regexp = "^[A-Za-z0-9+_.-]+@(.+)$", message = "Invalid email format")
    private String email;
    
    public static void validate(Object obj) throws IllegalAccessException {
        Class<?> clazz = obj.getClass();
        
        for (Field field : clazz.getDeclaredFields()) {
            field.setAccessible(true);
            Object value = field.get(obj);
            
            // Check @NotNull
            if (field.isAnnotationPresent(NotNull.class)) {
                if (value == null) {
                    NotNull notNull = field.getAnnotation(NotNull.class);
                    throw new ValidationException(field.getName() + ": " + 
                        notNull.message());
                }
            }
            
            // Check @Size
            if (field.isAnnotationPresent(Size.class) && value instanceof String) {
                Size size = field.getAnnotation(Size.class);
                String strValue = (String) value;
                if (strValue.length() < size.min() || strValue.length() > size.max()) {
                    String message = size.message()
                        .replace("{min}", String.valueOf(size.min()))
                        .replace("{max}", String.valueOf(size.max()));
                    throw new ValidationException(field.getName() + ": " + message);
                }
            }
            
            // Check @Pattern
            if (field.isAnnotationPresent(Pattern.class) && value instanceof String) {
                Pattern pattern = field.getAnnotation(Pattern.class);
                if (!((String) value).matches(pattern.regexp())) {
                    throw new ValidationException(field.getName() + ": " + 
                        pattern.message().replace("{regexp}", pattern.regexp()));
                }
            }
        }
    }
}

// Type Annotations (Java 8+)
public class TypeAnnotations {
    @NonNull String name;
    List<@NonNull String> strings;
    
    public void method(@NonNull String param) {
        @NonNull String local = "value";
    }
    
    public void genericMethod() {
        List<@Nullable String> nullableStrings = new ArrayList<>();
        Map<@NonNull String, @Nullable Integer> map = new HashMap<>();
    }
}

// Custom annotation for dependency injection
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Inject {
    String name() default "";
}

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Component {
    String value() default "";
}

// Simple DI Container using annotations
public class SimpleDIContainer {
    private Map<String, Object> beans = new HashMap<>();
    
    public void registerBean(String name, Object bean) {
        beans.put(name, bean);
    }
    
    public void autowire(Object target) throws IllegalAccessException {
        Class<?> clazz = target.getClass();
        
        for (Field field : clazz.getDeclaredFields()) {
            if (field.isAnnotationPresent(Inject.class)) {
                Inject inject = field.getAnnotation(Inject.class);
                String beanName = inject.name().isEmpty() ? 
                    field.getType().getSimpleName().toLowerCase() : inject.name();
                
                Object bean = beans.get(beanName);
                if (bean != null) {
                    field.setAccessible(true);
                    field.set(target, bean);
                }
            }
        }
    }
}

class ValidationException extends RuntimeException {
    public ValidationException(String message) {
        super(message);
    }
}

class DataAccessException extends Exception {
    public DataAccessException(String message) {
        super(message);
    }
}

// Annotation for generation
@Retention(RetentionPolicy.SOURCE)
@Target(ElementType.TYPE)
@interface GenerateBuilder {
}

// Type use annotations
@Target(ElementType.TYPE_USE)
@Retention(RetentionPolicy.RUNTIME)
@interface NonNull {}

@Target(ElementType.TYPE_USE)
@Retention(RetentionPolicy.RUNTIME)
@interface Nullable {}
```

### Interview Q&A

**Q1: What are the differences between annotation retention policies?**
- **SOURCE**: Used by compiler only, not in bytecode (e.g., @Override)
- **CLASS**: In bytecode but not available at runtime (default)
- **RUNTIME**: Available via reflection at runtime (e.g., @Entity)

**Q2: How do you create a custom annotation?**
Use @interface keyword, define elements as methods, specify meta-annotations (@Target, @Retention), provide default values if needed.

**Q3: What is the purpose of @FunctionalInterface?**
Indicates that an interface is intended to be functional (single abstract method). Compiler enforces this constraint, preventing accidental addition of abstract methods.

**Q4: How can annotations be processed?**
- Compile-time: Using annotation processors (extends AbstractProcessor)
- Runtime: Using reflection API to read annotation values
- Build tools: Maven/Gradle plugins can process annotations

---

## Chapter 26: Secure Coding

### Cornell Notes

| **Key Concepts** | **Detailed Explanations** |
|-----------------|---------------------------|
| **Security Principles** | • Least privilege: Minimal necessary access<br>• Defense in depth: Multiple security layers<br>• Fail securely: Safe failure modes<br>• Don't trust input: Validate everything<br>• Separation of duties |
| **Input Validation** | • Whitelist validation preferred<br>• Validate type, length, format, range<br>• Canonicalization<br>• Reject suspicious input<br>• Server-side validation mandatory |
| **SQL Injection** | • Use parameterized queries<br>• Avoid string concatenation<br>• Stored procedures<br>• Input validation<br>• Least privilege database users |
| **XSS Prevention** | • Output encoding<br>• Context-aware escaping<br>• Content Security Policy<br>• Input validation<br>• HTTPOnly cookies |
| **Authentication** | • Strong password policies<br>• Multi-factor authentication<br>• Secure password storage (bcrypt, scrypt)<br>• Session management<br>• Account lockout mechanisms |
| **Cryptography** | • Use standard algorithms<br>• Secure random numbers<br>• Key management<br>• Don't roll your own crypto<br>• TLS/SSL for transport |
| **Sensitive Data** | • Encryption at rest and in transit<br>• Secure storage<br>• Clear from memory<br>• Avoid logging sensitive data<br>• Data classification |
| **Error Handling** | • Don't expose internal details<br>• Generic error messages<br>• Log security events<br>• Fail closed, not open |

### Code Examples

```java
import java.security.*;
import javax.crypto.*;
import javax.crypto.spec.*;
import java.util.Base64;
import java.security.spec.*;
import org.mindrot.jbcrypt.BCrypt;

// Input Validation
public class InputValidation {
    // Whitelist validation
    public static boolean validateUsername(String username) {
        // Only alphanumeric and underscore, 3-20 characters
        String pattern = "^[a-zA-Z0-9_]{3,20}$";
        return username != null && username.matches(pattern);
    }
    
    public static boolean validateEmail(String email) {
        // Simple email pattern
        String pattern = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$";
        return email != null && email.matches(pattern);
    }
    
    public static String sanitizeHtml(String input) {
        if (input == null) return null;
        
        return input
            .replace("&", "&amp;")
            .replace("<", "&lt;")
            .replace(">", "&gt;")
            .replace("\"", "&quot;")
            .replace("'", "&#x27;")
            .replace("/", "&#x2F;");
    }
    
    // Path traversal prevention
    public static boolean isValidFilename(String filename) {
        if (filename == null) return false;
        
        // Reject path traversal attempts
        if (filename.contains("..") || 
            filename.contains("/") || 
            filename.contains("\\")) {
            return false;
        }
        
        // Whitelist allowed characters
        return filename.matches("^[a-zA-Z0-9._-]+$");
    }
    
    // Numeric range validation
    public static boolean validateAge(int age) {
        return age >= 0 && age <= 150;
    }
    
    // Command injection prevention
    public static String[] buildCommand(String userInput) {
        // Never use Runtime.exec(String) with user input
        // Use array form and validate input
        if (!userInput.matches("^[a-zA-Z0-9]+$")) {
            throw new IllegalArgumentException("Invalid input");
        }
        
        return new String[]{"program", "--option", userInput};
    }
}

// SQL Injection Prevention
public class SQLInjectionPrevention {
    // WRONG - Vulnerable to SQL injection
    public void vulnerableQuery(Connection conn, String username) 
            throws SQLException {
        String sql = "SELECT * FROM users WHERE username = '" + username + "'";
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery(sql);  // DANGEROUS!
    }
    
    // CORRECT - Using PreparedStatement
    public void safeQuery(Connection conn, String username) 
            throws SQLException {
        String sql = "SELECT * FROM users WHERE username = ?";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, username);  // Safe parameterization
            try (ResultSet rs = pstmt.executeQuery()) {
                // Process results
            }
        }
    }
    
    // Safe stored procedure call
    public void callStoredProcedure(Connection conn, long userId) 
            throws SQLException {
        String sql = "{call getUserInfo(?)}";
        try (CallableStatement cstmt = conn.prepareCall(sql)) {
            cstmt.setLong(1, userId);
            cstmt.execute();
        }
    }
}

// Password Security
public class PasswordSecurity {
    // Password hashing with bcrypt
    public static String hashPassword(String password) {
        // Generate salt and hash with bcrypt (cost factor 12)
        return BCrypt.hashpw(password, BCrypt.gensalt(12));
    }
    
    public static boolean verifyPassword(String password, String hash) {
        return BCrypt.checkpw(password, hash);
    }
    
    // Password strength validation
    public static boolean isStrongPassword(String password) {
        if (password == null || password.length() < 8) {
            return false;
        }
        
        boolean hasUpper = false;
        boolean hasLower = false;
        boolean hasDigit = false;
        boolean hasSpecial = false;
        
        for (char c : password.toCharArray()) {
            if (Character.isUpperCase(c)) hasUpper = true;
            else if (Character.isLowerCase(c)) hasLower = true;
            else if (Character.isDigit(c)) hasDigit = true;
            else if (!Character.isLetterOrDigit(c)) hasSpecial = true;
        }
        
        return hasUpper && hasLower && hasDigit && hasSpecial;
    }
}

// Secure Random Number Generation
public class SecureRandomExample {
    private static final SecureRandom secureRandom = new SecureRandom();
    
    public static String generateSessionId() {
        byte[] bytes = new byte[32];
        secureRandom.nextBytes(bytes);
        return Base64.getUrlEncoder().withoutPadding().encodeToString(bytes);
    }
    
    public static String generateToken(int length) {
        String chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        StringBuilder token = new StringBuilder(length);
        
        for (int i = 0; i < length; i++) {
            token.append(chars.charAt(secureRandom.nextInt(chars.length())));
        }
        
        return token.toString();
    }
    
    public static int generateOTP() {
        // Generate 6-digit OTP
        return 100000 + secureRandom.nextInt(900000);
    }
}

// Encryption and Decryption
public class EncryptionExample {
    private static final String ALGORITHM = "AES/GCM/NoPadding";
    private static final int KEY_SIZE = 256;
    private static final int IV_SIZE = 12;
    private static final int TAG_SIZE = 128;
    
    public static SecretKey generateKey() throws NoSuchAlgorithmException {
        KeyGenerator keyGen = KeyGenerator.getInstance("AES");
        keyGen.init(KEY_SIZE);
        return keyGen.generateKey();
    }
    
    public static String encrypt(String plaintext, SecretKey key) 
            throws Exception {
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        
        // Generate IV
        byte[] iv = new byte[IV_SIZE];
        new SecureRandom().nextBytes(iv);
        
        GCMParameterSpec spec = new GCMParameterSpec(TAG_SIZE, iv);
        cipher.init(Cipher.ENCRYPT_MODE, key, spec);
        
        byte[] ciphertext = cipher.doFinal(plaintext.getBytes("UTF-8"));
        
        // Combine IV and ciphertext
        byte[] combined = new byte[iv.length + ciphertext.length];
        System.arraycopy(iv, 0, combined, 0, iv.length);
        System.arraycopy(ciphertext, 0, combined, iv.length, ciphertext.length);
        
        return Base64.getEncoder().encodeToString(combined);
    }
    
    public static String decrypt(String encryptedData, SecretKey key) 
            throws Exception {
        byte[] combined = Base64.getDecoder().decode(encryptedData);
        
        // Extract IV
        byte[] iv = new byte[IV_SIZE];
        System.arraycopy(combined, 0, iv, 0, iv.length);
        
        // Extract ciphertext
        byte[] ciphertext = new byte[combined.length - IV_SIZE];
        System.arraycopy(combined, IV_SIZE, ciphertext, 0, ciphertext.length);
        
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        GCMParameterSpec spec = new GCMParameterSpec(TAG_SIZE, iv);
        cipher.init(Cipher.DECRYPT_MODE, key, spec);
        
        byte[] plaintext = cipher.doFinal(ciphertext);
        return new String(plaintext, "UTF-8");
    }
}

// Secure Session Management
public class SessionManagement {
    private static final Map<String, Session> sessions = new ConcurrentHashMap<>();
    private static final int SESSION_TIMEOUT = 30 * 60; // 30 minutes
    
    public static class Session {
        private final String id;
        private final String userId;
        private final long createdAt;
        private long lastAccessedAt;
        private final String ipAddress;
        
        public Session(String userId, String ipAddress) {
            this.id = SecureRandomExample.generateSessionId();
            this.userId = userId;
            this.ipAddress = ipAddress;
            this.createdAt = System.currentTimeMillis();
            this.lastAccessedAt = createdAt;
        }
        
        public boolean isValid(String ipAddress) {
            long now = System.currentTimeMillis();
            long elapsed = (now - lastAccessedAt) / 1000;
            
            // Check timeout and IP address
            return elapsed < SESSION_TIMEOUT && this.ipAddress.equals(ipAddress);
        }
        
        public void updateLastAccessed() {
            this.lastAccessedAt = System.currentTimeMillis();
        }
    }
    
    public static Session createSession(String userId, String ipAddress) {
        Session session = new Session(userId, ipAddress);
        sessions.put(session.id, session);
        return session;
    }
    
    public static Session getSession(String sessionId, String ipAddress) {
        Session session = sessions.get(sessionId);
        
        if (session != null && session.isValid(ipAddress)) {
            session.updateLastAccessed();
            return session;
        } else {
            sessions.remove(sessionId);
            return null;
        }
    }
    
    public static void invalidateSession(String sessionId) {
        sessions.remove(sessionId);
    }
    
    // Clean up expired sessions
    public static void cleanupSessions() {
        long now = System.currentTimeMillis();
        sessions.entrySet().removeIf(entry -> {
            long elapsed = (now - entry.getValue().lastAccessedAt) / 1000;
            return elapsed > SESSION_TIMEOUT;
        });
    }
}

// Secure File Operations
public class SecureFileOperations {
    private static final String UPLOAD_DIR = "/secure/uploads/";
    private static final long MAX_FILE_SIZE = 10 * 1024 * 1024; // 10MB
    private static final Set<String> ALLOWED_EXTENSIONS = 
        Set.of("jpg", "png", "pdf", "txt");
    
    public static void saveUploadedFile(byte[] fileData, String filename) 
            throws IOException {
        // Validate filename
        if (!InputValidation.isValidFilename(filename)) {
            throw new SecurityException("Invalid filename");
        }
        
        // Check file size
        if (fileData.length > MAX_FILE_SIZE) {
            throw new SecurityException("File too large");
        }
        
        // Check extension
        String extension = getFileExtension(filename);
        if (!ALLOWED_EXTENSIONS.contains(extension.toLowerCase())) {
            throw new SecurityException("File type not allowed");
        }
        
        // Generate safe filename
        String safeFilename = UUID.randomUUID().toString() + "." + extension;
        Path path = Paths.get(UPLOAD_DIR + safeFilename);
        
        // Ensure path is within upload directory
        if (!path.normalize().startsWith(UPLOAD_DIR)) {
            throw new SecurityException("Invalid path");
        }
        
        // Write file with restricted permissions
        Files.write(path, fileData);
        
        // Set file permissions (Unix-like systems)
        Set<PosixFilePermission> perms = EnumSet.of(
            PosixFilePermission.OWNER_READ,
            PosixFilePermission.OWNER_WRITE
        );
        Files.setPosixFilePermissions(path, perms);
    }
    
    private static String getFileExtension(String filename) {
        int lastDot = filename.lastIndexOf('.');
        return lastDot > 0 ? filename.substring(lastDot + 1) : "";
    }
}

// Security Headers
public class SecurityHeaders {
    public static void setSecurityHeaders(HttpServletResponse response) {
        // Prevent XSS
        response.setHeader("X-XSS-Protection", "1; mode=block");
        response.setHeader("X-Content-Type-Options", "nosniff");
        
        // Prevent clickjacking
        response.setHeader("X-Frame-Options", "DENY");
        
        // Content Security Policy
        response.setHeader("Content-Security-Policy", 
            "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'");
        
        // HTTPS enforcement
        response.setHeader("Strict-Transport-Security", 
            "max-age=31536000; includeSubDomains");
        
        // Referrer policy
        response.setHeader("Referrer-Policy", "strict-origin-when-cross-origin");
        
        // Permissions policy
        response.setHeader("Permissions-Policy", 
            "geolocation=(), microphone=(), camera=()");
    }
}

// Logging Security Events
public class SecurityLogger {
    private static final Logger logger = LoggerFactory.getLogger(SecurityLogger.class);
    
    public static void logLoginAttempt(String username, boolean success, String ip) {
        if (success) {
            logger.info("Successful login - User: {}, IP: {}", 
                sanitizeForLog(username), ip);
        } else {
            logger.warn("Failed login attempt - User: {}, IP: {}", 
                sanitizeForLog(username), ip);
        }
    }
    
    public static void logSecurityException(String message, Exception e) {
        // Don't log sensitive data
        logger.error("Security exception: {}", sanitizeForLog(message), e);
    }
    
    private static String sanitizeForLog(String input) {
        if (input == null) return "null";
        // Remove line breaks to prevent log injection
        return input.replaceAll("[\r\n]", "_");
    }
}

// Example interfaces for compilation
interface HttpServletResponse {
    void setHeader(String name, String value);
}

interface Logger {
    void info(String format, Object... arguments);
    void warn(String format, Object... arguments);
    void error(String format, Object... arguments);
}

class LoggerFactory {
    static Logger getLogger(Class<?> clazz) {
        return new Logger() {
            public void info(String format, Object... arguments) {}
            public void warn(String format, Object... arguments) {}
            public void error(String format, Object... arguments) {}
        };
    }
}
```

### Interview Q&A

**Q1: What is the principle of least privilege?**
Grant minimum levels of access or permissions needed to perform a function. Users, processes, and systems should only have access to resources necessary for their legitimate purpose.

**Q2: How do you prevent SQL injection?**
- Use parameterized queries/prepared statements
- Never concatenate user input into SQL
- Validate and sanitize input
- Use stored procedures where appropriate
- Apply least privilege to database accounts

**Q3: What are the OWASP Top 10 security risks?**
Common web application security risks including: Injection, Broken Authentication, Sensitive Data Exposure, XML External Entities, Broken Access Control, Security Misconfiguration, XSS, Insecure Deserialization, Using Components with Known Vulnerabilities, Insufficient Logging.

**Q4: How should passwords be stored?**
Never store plain text passwords. Use strong, slow hashing algorithms like bcrypt, scrypt, or Argon2 with proper salt. These are designed to be computationally expensive to prevent brute force attacks.

**Q5: What is defense in depth?**
Layered security approach where multiple security controls are placed throughout a system. If one layer fails, others provide backup protection. Examples: firewalls, encryption, access controls, monitoring.


---

## Comprehensive Interview Q&A Bank

### Core Java Fundamentals

**Q: Explain the main principles of OOP.**
- **Encapsulation**: Hide implementation details, expose interface
- **Inheritance**: Reuse code through parent-child relationships
- **Polymorphism**: One interface, multiple implementations
- **Abstraction**: Hide complexity, show essential features

**Q: What happens when you don't override equals() and hashCode()?**
Default Object implementation compares references for equals() and uses memory address for hashCode(). Issues arise in collections like HashMap.

**Q: Explain pass-by-value in Java.**
Java is always pass-by-value. For objects, the reference value is passed, not the object itself. Changes to object state persist, but reassigning the reference doesn't affect the caller.

### Collections & Generics

**Q: How does HashMap handle collisions?**
Uses chaining with linked lists. In Java 8+, converts to balanced tree (red-black tree) when chain length exceeds 8 for better performance.

**Q: What is type erasure?**
Generic type information is removed at runtime, replaced with bounds or Object. Enables backward compatibility but limits runtime type information.

**Q: Explain fail-fast vs fail-safe iterators.**
- **Fail-fast**: Throw ConcurrentModificationException if collection modified during iteration (ArrayList, HashMap)
- **Fail-safe**: Work on copy, don't throw exception (CopyOnWriteArrayList, ConcurrentHashMap)

### Concurrency

**Q: What is thread starvation?**
A thread is unable to gain regular access to shared resources and makes little or no progress, typically due to greedy threads or unfair scheduling.

**Q: Explain volatile keyword.**
Ensures visibility of changes across threads, prevents caching in thread-local memory. Doesn't provide atomicity for compound operations.

**Q: What's the difference between synchronized and Lock?**
- **synchronized**: Implicit, automatic release, no timeout
- **Lock**: Explicit, manual release, tryLock with timeout, multiple conditions

### Memory Management

**Q: Describe Java memory areas.**
- **Heap**: Objects, shared across threads, divided into Young (Eden, Survivor) and Old generation
- **Stack**: Method calls, local variables, thread-specific
- **Method Area/Metaspace**: Class metadata, static variables
- **PC Registers**: Current instruction per thread
- **Native Method Stack**: Native method execution

**Q: What causes OutOfMemoryError?**
- Heap space exhaustion
- PermGen/Metaspace full
- Unable to create native threads
- Array size exceeds platform limit
- Direct memory exhaustion

**Q: Explain strong, weak, soft, and phantom references.**
- **Strong**: Normal references, prevent GC
- **Soft**: Cleared before OutOfMemoryError
- **Weak**: Cleared on next GC cycle
- **Phantom**: Notification before finalization

### Java 8+ Features

**Q: What are the main features introduced in Java 8?**
- Lambda expressions
- Stream API
- Optional class
- Default methods in interfaces
- Method references
- New Date/Time API (java.time)
- CompletableFuture

**Q: Explain the difference between map() and flatMap() in streams.**
- **map()**: One-to-one transformation, preserves stream structure
- **flatMap()**: One-to-many transformation, flattens nested streams

**Q: What improvements were made to interfaces in Java 8 and 9?**
- **Java 8**: Default and static methods
- **Java 9**: Private methods for code reuse within interface

### Exception Handling

**Q: Can you catch multiple exceptions in one catch block?**
Yes, using multi-catch with pipe separator: `catch (IOException | SQLException e)`

**Q: What is exception chaining?**
Wrapping one exception in another to preserve the original cause while throwing a different exception type.

**Q: Explain the difference between final, finally, and finalize.**
- **final**: Keyword for constants, prevent inheritance/overriding
- **finally**: Block that always executes after try-catch
- **finalize()**: Deprecated method called before garbage collection

### Design Patterns & Best Practices

**Q: Implement Singleton pattern in Java.**
```java
public enum SingletonEnum {
    INSTANCE;
    // Best approach - thread-safe, serialization-safe
}

public class SingletonDoubleCheck {
    private static volatile SingletonDoubleCheck instance;
    
    private SingletonDoubleCheck() {}
    
    public static SingletonDoubleCheck getInstance() {
        if (instance == null) {
            synchronized (SingletonDoubleCheck.class) {
                if (instance == null) {
                    instance = new SingletonDoubleCheck();
                }
            }
        }
        return instance;
    }
}
```

**Q: What is the Builder pattern and when to use it?**
Used for constructing complex objects with many optional parameters. Provides fluent API, immutability, and clear object construction.

**Q: Explain SOLID principles.**
- **S**ingle Responsibility: One reason to change
- **O**pen/Closed: Open for extension, closed for modification
- **L**iskov Substitution: Subtypes must be substitutable
- **I**nterface Segregation: Many specific interfaces
- **D**ependency Inversion: Depend on abstractions

### Performance & Optimization

**Q: How do you identify memory leaks in Java?**
- Monitor heap usage over time
- Use profilers (JProfiler, YourKit)
- Analyze heap dumps
- Look for growing collections, unclosed resources, static references

**Q: What are the best practices for string concatenation?**
- Use StringBuilder for loops
- Use + for simple concatenations (compiler optimizes)
- String.format() for complex formatting
- String.join() for collections

**Q: Explain JIT compilation.**
Just-In-Time compilation converts frequently executed bytecode to native machine code at runtime for performance optimization.

### Database & JDBC

**Q: What are the JDBC connection steps?**
1. Load driver (automatic in JDBC 4.0+)
2. Establish connection
3. Create statement
4. Execute query
5. Process results
6. Close resources

**Q: Explain PreparedStatement vs Statement.**
- **PreparedStatement**: Precompiled, prevents SQL injection, better for repeated execution
- **Statement**: Simple queries, vulnerable to SQL injection

**Q: What is connection pooling?**
Reuses database connections instead of creating new ones, improving performance by reducing connection overhead.

### Spring Framework Integration

**Q: What is dependency injection?**
Design pattern where objects receive dependencies from external sources rather than creating them, promoting loose coupling.

**Q: Explain @Autowired, @Component, @Service, @Repository.**
- **@Autowired**: Inject dependencies
- **@Component**: Generic Spring bean
- **@Service**: Business logic layer
- **@Repository**: Data access layer with exception translation

### Microservices & Modern Java

**Q: What features make Java suitable for microservices?**
- Module system for better encapsulation
- Lightweight frameworks (Spring Boot, Micronaut)
- Container support (Docker)
- GraalVM for native images
- Reactive programming support

**Q: Explain RESTful principles.**
- **Stateless**: No client context on server
- **Client-Server**: Separation of concerns
- **Cacheable**: Responses can be cached
- **Uniform Interface**: Standard HTTP methods
- **Layered System**: Architecture layers

### Testing

**Q: What is the difference between unit, integration, and system testing?**
- **Unit**: Test individual components in isolation
- **Integration**: Test component interactions
- **System**: Test complete application flow

**Q: Explain TDD (Test-Driven Development).**
Write tests first, then code to pass tests. Red-Green-Refactor cycle: fail, pass, improve.

**Q: What are mock objects?**
Simulated objects that mimic real object behavior for testing in isolation.

---

## Quick Reference Summary

### Java Keywords Quick Reference

| Category | Keywords |
|----------|----------|
| **Access Modifiers** | `public`, `private`, `protected`, (package-private) |
| **Class/Method Modifiers** | `abstract`, `final`, `static`, `synchronized`, `native`, `strictfp`, `transient`, `volatile` |
| **Flow Control** | `if`, `else`, `switch`, `case`, `default`, `for`, `while`, `do`, `break`, `continue`, `return` |
| **Exception Handling** | `try`, `catch`, `finally`, `throw`, `throws` |
| **Class Related** | `class`, `interface`, `extends`, `implements`, `enum`, `record`, `sealed`, `permits` |
| **Object/Variable** | `new`, `this`, `super`, `instanceof`, `var` |
| **Package** | `package`, `import` |
| **Primitives** | `boolean`, `byte`, `char`, `short`, `int`, `long`, `float`, `double` |
| **Other** | `void`, `null`, `true`, `false`, `const*`, `goto*` |

*Reserved but not used

### Collection Hierarchy Cheat Sheet

```
Collection
├── List
│   ├── ArrayList
│   ├── LinkedList
│   ├── Vector
│   └── Stack
├── Set
│   ├── HashSet
│   ├── LinkedHashSet
│   └── SortedSet
│       └── NavigableSet
│           └── TreeSet
└── Queue
    ├── PriorityQueue
    ├── LinkedList
    └── Deque
        ├── ArrayDeque
        └── LinkedList

Map
├── HashMap
├── LinkedHashMap
├── Hashtable
└── SortedMap
    └── NavigableMap
        └── TreeMap
```

### Time Complexity Reference

| Operation | ArrayList | LinkedList | HashSet | TreeSet | HashMap | TreeMap |
|-----------|-----------|------------|---------|---------|---------|---------|
| **Access** | O(1) | O(n) | - | - | - | - |
| **Search** | O(n) | O(n) | O(1) | O(log n) | O(1) | O(log n) |
| **Insert** | O(n)* | O(1) | O(1) | O(log n) | O(1) | O(log n) |
| **Delete** | O(n) | O(1) | O(1) | O(log n) | O(1) | O(log n) |

*Amortized O(1) at end

### Stream Operations Quick Reference

**Intermediate Operations (Lazy)**
- `filter(Predicate)` - Keep matching elements
- `map(Function)` - Transform elements
- `flatMap(Function)` - Transform and flatten
- `distinct()` - Remove duplicates
- `sorted()` - Sort elements
- `sorted(Comparator)` - Sort with comparator
- `limit(long)` - Limit stream size
- `skip(long)` - Skip elements
- `peek(Consumer)` - Debug/side effects

**Terminal Operations (Eager)**
- `forEach(Consumer)` - Process each element
- `count()` - Count elements
- `collect(Collector)` - Collect to collection
- `reduce(BinaryOperator)` - Reduce to single value
- `findFirst()` - First element
- `findAny()` - Any element
- `allMatch(Predicate)` - All match
- `anyMatch(Predicate)` - Any matches
- `noneMatch(Predicate)` - None match
- `min/max(Comparator)` - Min/max element

### Lambda Syntax Quick Reference

```java
// No parameters
() -> System.out.println("Hello")

// One parameter (parentheses optional)
x -> x * 2
(x) -> x * 2

// Multiple parameters
(x, y) -> x + y

// With type declaration
(int x, int y) -> x + y

// Multi-line body
(x, y) -> {
    int sum = x + y;
    return sum;
}

// Method reference alternatives
System.out::println     // Instance method
String::toUpperCase     // Instance method on parameter
Integer::parseInt       // Static method
ArrayList::new          // Constructor
int[]::new             // Array constructor
```

### Date/Time Format Patterns

| Pattern | Description | Example |
|---------|-------------|---------|
| `y` | Year | 2024 |
| `M` | Month | 7, 07, Jul, July |
| `d` | Day of month | 9, 09 |
| `E` | Day of week | Tue, Tuesday |
| `H` | Hour (0-23) | 13 |
| `h` | Hour (1-12) | 1 |
| `m` | Minute | 30 |
| `s` | Second | 55 |
| `a` | AM/PM | PM |
| `z` | Time zone | PST, GMT+08:00 |

### Exception Hierarchy

```
Throwable
├── Error (Don't catch)
│   ├── VirtualMachineError
│   │   ├── OutOfMemoryError
│   │   └── StackOverflowError
│   └── AssertionError
└── Exception
    ├── RuntimeException (Unchecked)
    │   ├── NullPointerException
    │   ├── IllegalArgumentException
    │   ├── IllegalStateException
    │   ├── IndexOutOfBoundsException
    │   ├── ClassCastException
    │   └── ArithmeticException
    └── Checked Exceptions
        ├── IOException
        ├── SQLException
        ├── ClassNotFoundException
        └── InterruptedException
```

### Functional Interfaces Summary

| Interface | Method | Input | Output | Example |
|-----------|--------|-------|--------|---------|
| `Supplier<T>` | `get()` | None | T | `() -> "Hello"` |
| `Consumer<T>` | `accept(T)` | T | void | `x -> System.out.println(x)` |
| `Predicate<T>` | `test(T)` | T | boolean | `x -> x > 0` |
| `Function<T,R>` | `apply(T)` | T | R | `x -> x.toString()` |
| `UnaryOperator<T>` | `apply(T)` | T | T | `x -> x * 2` |
| `BiFunction<T,U,R>` | `apply(T,U)` | T,U | R | `(x,y) -> x + y` |
| `BinaryOperator<T>` | `apply(T,T)` | T,T | T | `(x,y) -> x * y` |

### Module Directives Summary

| Directive | Purpose | Example |
|-----------|---------|---------|
| `requires` | Declare dependency | `requires java.sql;` |
| `requires transitive` | Transitive dependency | `requires transitive java.logging;` |
| `exports` | Export package | `exports com.example.api;` |
| `exports...to` | Qualified export | `exports com.example.internal to com.test;` |
| `opens` | Open for reflection | `opens com.example.model;` |
| `opens...to` | Qualified open | `opens com.example.config to spring.core;` |
| `uses` | Service consumer | `uses com.example.Service;` |
| `provides...with` | Service provider | `provides Service with ServiceImpl;` |

### JDBC Best Practices

```java
// Try-with-resources for automatic cleanup
String sql = "SELECT * FROM users WHERE id = ?";
try (Connection conn = dataSource.getConnection();
     PreparedStatement pstmt = conn.prepareStatement(sql)) {
    
    pstmt.setLong(1, userId);
    
    try (ResultSet rs = pstmt.executeQuery()) {
        while (rs.next()) {
            // Process results
        }
    }
} catch (SQLException e) {
    // Handle exception
}
```

### Concurrency Utilities Comparison

| Class | Purpose | Key Features |
|-------|---------|--------------|
| `synchronized` | Basic synchronization | Simple, automatic |
| `ReentrantLock` | Advanced locking | Timeout, interruptible |
| `Semaphore` | Resource limiting | Multiple permits |
| `CountDownLatch` | One-time barrier | Count down to zero |
| `CyclicBarrier` | Reusable barrier | Reset after use |
| `Phaser` | Dynamic barrier | Variable parties |
| `Exchanger` | Thread data exchange | Swap data between threads |

### JVM Flags Quick Reference

| Flag | Purpose |
|------|---------|
| `-Xms` | Initial heap size |
| `-Xmx` | Maximum heap size |
| `-XX:NewRatio` | Old/Young generation ratio |
| `-XX:+UseG1GC` | Use G1 garbage collector |
| `-XX:+PrintGCDetails` | Print GC details |
| `-Xss` | Thread stack size |
| `-XX:MaxMetaspaceSize` | Maximum metaspace |
| `-ea` | Enable assertions |
| `-verbose:gc` | Verbose GC output |

### Regular Expression Patterns

| Pattern | Meaning |
|---------|---------|
| `.` | Any character |
| `*` | Zero or more |
| `+` | One or more |
| `?` | Zero or one |
| `^` | Start of line |
| `$` | End of line |
| `\d` | Digit [0-9] |
| `\D` | Non-digit |
| `\s` | Whitespace |
| `\S` | Non-whitespace |
| `\w` | Word character [a-zA-Z0-9_] |
| `\W` | Non-word character |
| `[abc]` | Character class |
| `[^abc]` | Negated class |
| `(x\|y)` | Alternation |

### Design Pattern Templates

**Singleton (Thread-Safe)**
```java
public enum Singleton {
    INSTANCE;
    public void doSomething() { }
}
```

**Factory Method**
```java
public interface Product { }
public class ConcreteProduct implements Product { }

public abstract class Creator {
    public abstract Product createProduct();
}
```

**Builder**
```java
public class Product {
    private final String field1;
    private final String field2;
    
    private Product(Builder builder) {
        this.field1 = builder.field1;
        this.field2 = builder.field2;
    }
    
    public static class Builder {
        private String field1;
        private String field2;
        
        public Builder field1(String val) {
            field1 = val;
            return this;
        }
        
        public Product build() {
            return new Product(this);
        }
    }
}
```

**Observer**
```java
public interface Observer {
    void update(String message);
}

public class Subject {
    private List<Observer> observers = new ArrayList<>();
    
    public void attach(Observer o) {
        observers.add(o);
    }
    
    public void notifyObservers(String message) {
        observers.forEach(o -> o.update(message));
    }
}
```

### Memory Management Tips

1. **Avoid Memory Leaks**
   - Close resources (try-with-resources)
   - Remove listeners/callbacks
   - Clear collections when done
   - Avoid static collections of objects

2. **Optimize String Usage**
   - Use StringBuilder for concatenation in loops
   - Intern strings when appropriate
   - Avoid creating unnecessary String objects

3. **Collection Sizing**
   - Initialize collections with expected size
   - Use appropriate collection types
   - Clear or null large collections when done

4. **Object Creation**
   - Reuse objects when possible
   - Use object pools for expensive objects
   - Avoid autoboxing in loops

### Performance Optimization Checklist

- [ ] Use appropriate data structures
- [ ] Minimize object creation
- [ ] Cache computed values
- [ ] Use lazy initialization
- [ ] Batch database operations
- [ ] Use prepared statements
- [ ] Implement proper equals/hashCode
- [ ] Use primitives over wrappers
- [ ] Profile before optimizing
- [ ] Consider parallel streams for large datasets

### Security Best Practices

1. **Input Validation**
   - Validate all inputs
   - Use parameterized queries
   - Sanitize user input
   - Implement rate limiting

2. **Authentication & Authorization**
   - Use strong passwords
   - Implement proper session management
   - Use HTTPS
   - Principle of least privilege

3. **Data Protection**
   - Encrypt sensitive data
   - Use secure random numbers
   - Clear sensitive data from memory
   - Implement proper logging (no sensitive data)

4. **Code Security**
   - Keep dependencies updated
   - Use security scanning tools
   - Follow OWASP guidelines
   - Regular security audits

### Testing Strategies

**Unit Testing**
```java
@Test
void testMethod() {
    // Arrange
    MyClass obj = new MyClass();
    
    // Act
    int result = obj.calculate(5);
    
    // Assert
    assertEquals(10, result);
}
```

**Integration Testing**
```java
@SpringBootTest
@AutoConfigureMockMvc
class IntegrationTest {
    @Autowired
    MockMvc mockMvc;
    
    @Test
    void testEndpoint() throws Exception {
        mockMvc.perform(get("/api/users"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$[0].name").exists());
    }
}
```

### Debugging Tips

1. **Use IDE Debugger**
   - Set breakpoints
   - Watch variables
   - Step through code
   - Evaluate expressions

2. **Logging**
   - Use appropriate log levels
   - Include context information
   - Use structured logging
   - Avoid logging in loops

3. **Profiling**
   - Memory profiling for leaks
   - CPU profiling for bottlenecks
   - Thread profiling for deadlocks
   - I/O profiling for slow operations

### Common Pitfalls to Avoid

1. **Comparing Strings with ==**
   ```java
   // Wrong
   if (str1 == str2)
   
   // Correct
   if (str1.equals(str2))
   ```

2. **Modifying Collection During Iteration**
   ```java
   // Wrong
   for (String item : list) {
       list.remove(item);
   }
   
   // Correct
   Iterator<String> it = list.iterator();
   while (it.hasNext()) {
       it.next();
       it.remove();
   }
   ```

3. **Not Closing Resources**
   ```java
   // Wrong
   FileInputStream fis = new FileInputStream("file.txt");
   
   // Correct
   try (FileInputStream fis = new FileInputStream("file.txt")) {
       // Use resource
   }
   ```

4. **Ignoring Thread Safety**
   ```java
   // Wrong
   private int counter = 0;
   public void increment() { counter++; }
   
   // Correct
   private AtomicInteger counter = new AtomicInteger(0);
   public void increment() { counter.incrementAndGet(); }
   ```

### Version-Specific Features Summary

**Java 8 (LTS)**
- Lambda expressions
- Stream API
- Optional
- Default methods
- Method references
- New Date/Time API

**Java 9**
- Module system
- JShell
- Private interface methods
- Collection factory methods
- Stream improvements

**Java 10**
- Local variable type inference (var)
- Application class-data sharing

**Java 11 (LTS)**
- String methods (isBlank, lines, repeat)
- Files.readString/writeString
- HTTP Client API
- Launch single-file programs

**Java 12-13**
- Switch expressions (preview)
- Text blocks (preview)

**Java 14**
- Switch expressions (standard)
- Records (preview)
- Pattern matching instanceof (preview)

**Java 15**
- Text blocks (standard)
- Sealed classes (preview)

**Java 16**
- Records (standard)
- Pattern matching instanceof (standard)

**Java 17 (LTS)**
- Sealed classes (standard)
- Pattern matching for switch (preview)
- Enhanced pseudo-random number generators

### Final Exam Preparation Tips

1. **Practice Coding**
   - Write code by hand
   - Focus on syntax details
   - Practice common algorithms
   - Understand compilation errors

2. **Review Topics**
   - Focus on new Java features
   - Understand collection framework
   - Master exception handling
   - Practice stream operations

3. **Time Management**
   - Read questions carefully
   - Skip difficult questions initially
   - Review all answers
   - Watch for trick questions

4. **Common Exam Tricks**
   - Missing semicolons/braces
   - Incorrect method signatures
   - Access modifier violations
   - Unreachable code
   - Uninitialized variables

---

## Conclusion

This comprehensive study guide covers all 26 chapters of the OCP Java SE 17 Developer certification. Key areas to focus on:

1. **Core Java**: Strong foundation in OOP, syntax, and basic concepts
2. **Collections & Generics**: Deep understanding of data structures
3. **Functional Programming**: Lambda expressions and Stream API
4. **Concurrency**: Thread management and synchronization
5. **I/O & NIO.2**: File operations and serialization
6. **Modules**: Understanding the module system
7. **Date/Time**: New java.time API

Remember:
- Practice coding regularly
- Understand concepts, don't just memorize
- Review official Oracle documentation
- Take practice exams
- Focus on Java 8-17 features

Good luck with your certification exam
