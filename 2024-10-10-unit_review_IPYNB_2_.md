---
layout: post
title: Unit 1-9 Review
description: Unit 1-9 Review through Code Snippets + Comments
type: ccc
categories: ['AP CSA']
permalink: /unit_review
comments: True
---

### Unit 1


```python
public class JavaTypes {

    public static void main(String[] args) {
        
        // Primitive types in Java are stored in the stack.
        // They are value types, meaning they hold actual values.
        
        // Integer primitive type (4 bytes)
        int myInt = 42;
        // Floating-point primitive type (4 bytes)
        float myFloat = 3.14f;
        // Double-precision floating point (8 bytes)
        double myDouble = 3.14159;
        // Character type (2 bytes)
        char myChar = 'A';
        // Boolean type (1 bit, JVM dependent)
        boolean myBoolean = true;
        
        // Reference types in Java are stored on the heap.
        // They hold the reference (or address) to the object in memory.
        
        // Example of a reference type: String (which is a class)
        String myString = "Hello, World!";
        
        // Arrays are also reference types, even for primitive arrays
        int[] myArray = {1, 2, 3, 4};
        
        // Memory Management:
        // The stack is used for storing primitive values and references to objects.
        // Each method call gets its own stack frame.
        // The heap is used for dynamic memory allocation, where objects (like arrays, Strings) are created.
        
        // Example:
        methodExample();
    }
    
    public static void methodExample() {
        // Local variables in this method are stored on the stack.
        int x = 100;  // This int variable is stored in the stack.
        
        // A new object is created, which is stored on the heap.
        // Only the reference (address) to this object is stored in the stack.
        String myNewString = new String("This is a new string.");
        
        // The stack will automatically free up memory once this method is done executing.
        // Objects in the heap will be garbage collected when they are no longer referenced.
    }
}

```

### Unit 2


```python
// This is a class definition in Java.
public class Car {

    // Class fields (or instance variables) hold the state of the object.
    private String model;  // Reference type, stored on the heap.
    private int year;      // Primitive type, stored in the heap as part of the object.

    // Constructor:
    // This special method is called when creating an object.
    // It initializes the object's state.
    public Car(String model, int year) {
        this.model = model; // The 'this' keyword refers to the current instance of the object.
        this.year = year;   // Assign the values passed to the constructor to the object fields.
    }

    // Void method:
    // This method performs an action but does not return a value.
    public void startCar() {
        System.out.println(model + " is starting...");
    }

    // Non-void method:
    // This method returns a value. In this case, it returns an int (the year).
    public int getCarYear() {
        return this.year;  // Return the year field of the Car object.
    }

    // Main method to demonstrate the use of the class, constructors, and methods.
    public static void main(String[] args) {
        
        // Creating an object (or instance) of the Car class.
        // This calls the constructor 'Car(String model, int year)'.
        Car myCar = new Car("Toyota Camry", 2021);
        
        // Calling a void method on the object:
        // This performs an action but does not return anything.
        myCar.startCar(); // Output: "Toyota Camry is starting..."

        // Calling a non-void method that returns a value:
        int carYear = myCar.getCarYear();  // Returns the car's year.
        System.out.println("Car year: " + carYear);  // Output: "Car year: 2021"
    }
}

```

### Unit 3 and 6


```python
public class IterationExamples {

    public static void main(String[] args) {

        // Example 1: For Loop
        // A 'for' loop is used when you know how many times you want to repeat a block of code.
        System.out.println("For Loop Example:");
        for (int i = 0; i < 5; i++) {
            System.out.println("i = " + i);  // Prints numbers 0 through 4
        }

        // Example 2: While Loop
        // A 'while' loop repeats as long as the condition is true.
        System.out.println("\nWhile Loop Example:");
        int counter = 0;
        while (counter < 5) {
            System.out.println("counter = " + counter);  // Prints numbers 0 through 4
            counter++;
        }

        // Example 3: Do-While Loop
        // A 'do-while' loop is similar to a 'while' loop, but it executes the loop body at least once.
        System.out.println("\nDo-While Loop Example:");
        int number = 0;
        do {
            System.out.println("number = " + number);  // Prints numbers 0 through 4
            number++;
        } while (number < 5);

        // Example 4: For-Each Loop (Enhanced For Loop)
        // A 'for-each' loop is used to iterate over arrays or collections (like lists).
        System.out.println("\nFor-Each Loop Example:");
        int[] numbers = {10, 20, 30, 40, 50};  // Array of integers
        for (int num : numbers) {
            System.out.println("num = " + num);  // Prints each element in the array
        }

        // Example 5: Nested For Loops
        // A nested loop is a loop inside another loop.
        System.out.println("\nNested For Loop Example (Multiplication Table):");
        for (int row = 1; row <= 3; row++) {  // Outer loop for rows
            for (int col = 1; col <= 3; col++) {  // Inner loop for columns
                System.out.print(row * col + "\t");  // Multiplying row by column
            }
            System.out.println();  // Move to the next line after each row
        }

        // Example 6: Break and Continue in Loops
        // 'break' exits the loop early, while 'continue' skips to the next iteration.
        System.out.println("\nBreak and Continue Example:");
        for (int i = 0; i < 10; i++) {
            if (i == 5) {
                break;  // Exit the loop when i is 5
            }
            if (i % 2 == 0) {
                continue;  // Skip even numbers
            }
            System.out.println("i = " + i);  // Prints only odd numbers up to 5
        }
    }
}

```

### Unit 4 and 5


```python
public class BankAccount {
    // Private fields (attributes of the class)
    private String accountHolderName;  // Stores the name of the account holder
    private double balance;            // Stores the balance of the account
    static int totalAccounts;          // Static variable to keep track of total number of accounts created

    // Parameterized constructor: initializes with account holder name and balance
    public BankAccount(String accountHolderName, double balance) {
        this.accountHolderName = accountHolderName;  // Assigns the provided account holder name
        this.balance = balance;                      // Assigns the provided balance
        totalAccounts += 1;                          // Increments the total number of accounts
    }

    // Non-parameterized constructor: initializes default values for the account holder and balance
    public BankAccount() {
        this.accountHolderName = "Unknown";  // Default name when none is provided
        this.balance = 0.0;                  // Default balance of 0.0
        totalAccounts += 1;                  // Increments the total number of accounts
    }

    // Mutator (setter) function: allows changing the account holder's name
    public void setAccountHolderName(String accountHolderName) {
        this.accountHolderName = accountHolderName;  // Updates the account holder name
    }

    // Mutator function: allows depositing money into the account
    public void deposit(double amount) {
        this.balance += amount;  // Adds the amount to the balance
    }

    // Mutator function: allows withdrawing money from the account
    public void withdraw(double amount) {
        this.balance -= amount;  // Subtracts the amount from the balance
    }

    // Accessor (getter) function: returns the name of the account holder
    public String getAccountHolderName() {
        return accountHolderName;  // Returns the account holder name
    }

    // Static accessor function: returns the total number of accounts created
    public static int getTotalAccounts() {
        return totalAccounts;  // Returns the static variable totalAccounts
    }

    // Accessor function: returns the balance of the account
    public double getBalance() {
        return balance;  // Returns the balance of the account
    }
}

// Creating instances of the BankAccount class
BankAccount account1 = new BankAccount();  // Using the non-parameterized constructor
BankAccount account2 = new BankAccount();  // Another instance with the non-parameterized constructor
BankAccount account3 = new BankAccount();  // Another instance with the non-parameterized constructor

// Setting the account holder's name and performing transactions
account1.setAccountHolderName("Anusha");
account1.deposit(10000.0);  // Depositing money
account1.withdraw(500.0);   // Withdrawing money

account2.setAccountHolderName("Avanthika");
account2.deposit(2000.0);   // Depositing money

account3.setAccountHolderName("Vibha");
account3.deposit(3000.0);   // Depositing money

// Displaying the details of each account
System.out.println("Account 1 - Name: " + account1.getAccountHolderName() + ", Balance: $" + account1.getBalance());
System.out.println("Account 2 - Name: " + account2.getAccountHolderName() + ", Balance: $" + account2.getBalance());
System.out.println("Account 3 - Name: " + account3.getAccountHolderName() + ", Balance: $" + account3.getBalance());

// Displaying the total number of accounts created
System.out.println("Total Accounts Created: " + BankAccount.getTotalAccounts());

```

### Unit 7 and 8


```python
public class ArrayExamples {

    public static void main(String[] args) {

        // Example 1: Creating and Accessing a 1D Array
        // A one-dimensional array holds a list of elements of the same data type.
        int[] oneDArray = {10, 20, 30, 40, 50};  // Array of 5 integers

        System.out.println("1D Array Elements:");
        for (int i = 0; i < oneDArray.length; i++) {
            System.out.println("Element at index " + i + ": " + oneDArray[i]);
        }

        // Example 2: Modifying a 1D Array
        // Accessing and changing an element in the array
        oneDArray[2] = 35;  // Changing the value at index 2
        System.out.println("\nUpdated 1D Array:");
        for (int i = 0; i < oneDArray.length; i++) {
            System.out.println("Element at index " + i + ": " + oneDArray[i]);
        }

        // Example 3: Creating and Accessing a 2D Array (Normal)
        // A 2D array (matrix) is an array of arrays, with each row having the same number of elements.
        int[][] twoDArray = {
            {1, 2, 3},    // Row 0
            {4, 5, 6},    // Row 1
            {7, 8, 9}     // Row 2
        };

        System.out.println("\n2D Array (Normal) Elements:");
        for (int row = 0; row < twoDArray.length; row++) {
            for (int col = 0; col < twoDArray[row].length; col++) {
                System.out.print(twoDArray[row][col] + " ");
            }
            System.out.println();  // Move to the next line after each row
        }

        // Example 4: Creating and Accessing a 2D Jagged Array
        // A jagged array is an array where the rows have different numbers of elements.
        int[][] jaggedArray = {
            {1, 2, 3},        // Row 0 (3 elements)
            {4, 5},           // Row 1 (2 elements)
            {6, 7, 8, 9}      // Row 2 (4 elements)
        };

        System.out.println("\n2D Jagged Array Elements:");
        for (int row = 0; row < jaggedArray.length; row++) {
            for (int col = 0; col < jaggedArray[row].length; col++) {
                System.out.print(jaggedArray[row][col] + " ");
            }
            System.out.println();  // Move to the next line after each row
        }

        // Example 5: Traversing a 2D Array Using Enhanced For-Each Loop
        System.out.println("\nTraversing 2D Array (Normal) using For-Each Loop:");
        for (int[] row : twoDArray) {
            for (int elem : row) {
                System.out.print(elem + " ");
            }
            System.out.println();  // Move to the next line after each row
        }

    }
}

```

# Unit 9


```python
// Parent class (Superclass)
class Animal {
    // Method that can be overridden
    public void sound() {
        System.out.println("This animal makes a sound");
    }

    // Method specific to the Animal class
    public void sleep() {
        System.out.println("This animal sleeps");
    }
}

// Child class (Subclass) inherits from Animal
class Dog extends Animal {
    // Overriding the sound method to give a specific behavior for dogs
    @Override
    public void sound() {
        System.out.println("The dog barks");
    }

    // Dog-specific method
    public void fetch() {
        System.out.println("The dog fetches the ball");
    }
}

// Another child class (Subclass) inherits from Animal
class Cat extends Animal {
    // Overriding the sound method to give a specific behavior for cats
    @Override
    public void sound() {
        System.out.println("The cat meows");
    }

    // Cat-specific method
    public void purr() {
        System.out.println("The cat is purring");
    }
}

public class Main {
    public static void main(String[] args) {
        // Creating an instance of the Dog class
        Dog dog = new Dog();
        dog.sound();  // Calls the overridden method in Dog
        dog.sleep();  // Calls the inherited method from Animal
        dog.fetch();  // Calls the Dog-specific method

        System.out.println();

        // Creating an instance of the Cat class
        Cat cat = new Cat();
        cat.sound();  // Calls the overridden method in Cat
        cat.sleep();  // Calls the inherited method from Animal
        cat.purr();   // Calls the Cat-specific method

        System.out.println();

        // Using polymorphism: Referencing Dog and Cat as Animals
        Animal myAnimal1 = new Dog();  // Animal reference, Dog object
        Animal myAnimal2 = new Cat();  // Animal reference, Cat object

        myAnimal1.sound();  // Calls Dog's overridden sound method
        myAnimal2.sound();  // Calls Cat's overridden sound method
    }
}

```

## MC Corrections

## FRQ Corrections
