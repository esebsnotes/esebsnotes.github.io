# Inheritance
Inheritance
~ process of deriving a new class from an existing one.


<!-- toc -->

- [Parent Class vs Child Class](#Parent-Class-vs-Child-Class)
  * [Parent Class](#Parent-Class)
  * [Child Class](#Child-Class)
  * [Example of Parent and Child](#Example-of-Parent-and-Child)
      - [Parent Class](#Parent-Class-1)
      - [Child Class](#Child-Class-1)
- [Access Modifiers](#Access-Modifiers)
- [Super](#Super)
  * [Example of Super](#Example-of-Super)
      - [Superclass](#Superclass)
      - [Subclasses](#Subclasses)
- [Override](#Override)
  * [Override Example](#Override-Example)
    + [Superclass](#Superclass-1)
    + [Subclass](#Subclass)
- [Object Class](#Object-Class)
  * [Example of Overriding Object Class](#Example-of-Overriding-Object-Class)
    + [equals()](#equals)
    + [toString()](#toString)
- [Glossary](#Glossary)

<!-- tocstop -->

## Parent Class vs Child Class
### Parent Class
Parent Class
~ super class
~ base class
```java
public class Parent {}
```
- Can't access the methods/data from child class (private or public)
- If not specified it extends Object class, contained in java.lang
- May have many subclasses (Child classes)


### Child Class
Child Class
~ class that "extends" a super class
~ sub class
~ derived class 

``` java
public class Child extends Parent {}
```
- Child class can only extend one Parent class
- Subclasses inherit the interface and implementation of their superclass
- Can access public data/methods of parent 
- Contains parents private data/methods, even though it can't call it 
  - May "get" or set private data using public methods

      ```java 
      public String getName()
       return name;
      ```
  
- Can call parent methods without qualification, like they are from child class (Instance data)
- Child classes follow an **is-a** relationship
  - A human is-a Mammal

- The subclass can also:
  - Hide 
    - (write a new methods/variables with the same name/signature)
  - Overload
  - Override 

---

### Example of Parent and Child 
##### Parent Class

```java
public class Vehicle {
  protected int wheels;
  protected void go()
}
```

##### Child Class

```java
public class Car extends Vehicle {
  private void drive() {
    int x = wheels;
    go();
  }
}
```

***

## Access Modifiers  


| Modifier| Class|Package|Subclass|World|
|--|:-:|:-:|:-:|:-:|
|public| Y | Y | Y | Y|
|protected| Y| Y | Y|N|
| default | Y| Y |N|N|
|private | Y | N |N | N|
> The default (no) modifier is also called "package private."

---

## Super  

super
~ access to parents members 
~ "this()" for parent class

- Common use: To invoke a parent's constructor
  - Has to be first 
  - Can use constructors with private parameters/data
  - Example:
    ```java
    super(instanceVariable)
    ```
- Can be used to invoke parent methods via dot-access
  - Example: 
    ```java
    super.parentMethod();
    ```
- Can be used to access immediate parent class instance variable
  - Example
      ```java
      super.parentInstanceVariable
      ```
- super() will be inserted if is not stated  
  - If a super class doesn't include a no-args, then the subclass constructors must include a super call
- Constructors are finished from "Top to bottom"
  - Parent class constructors are finished first
 

---

### Example of Super

##### Superclass

```java
public class Person {
  private String name;

  public Person(String name) {
    this.name = name;
  }
  
  public String getName() {
    return name;
  }
}
```  

##### Subclasses

```java
public class Student {
  protected int year;
  
  public Student(String name, int year) {
    super(name) //Can get the data, using getName()
    this.year = year;
  }
  
  public Student(String name) {
    this(name, -1); //Can use Constructor chaining
  }
}
```

```java 
public class Dentist extends Person {
  protected string degree;
  
  public Dentist(String name) {
    super(name);
    /*If not explixitaly stated in the first line of constructor,
    Java will insert super().
    Exception: If you have a chained call to another
    constructor in same class
    */
    degree = "DDS";
  }
}
```

---
## Override

Override
~ provide a new implementation for a method in the subclass.

- Overriding allows two objects related by inheritance to use the same naming convention for the methods that accomplish the same task different ways
- Static methods can be inherited, but not overridden (simple hides the superclass’ method)
- When a child class defines a method with the same signature as the parent, the child’s version overrides the parent. 
- @Override annotation before the method signature

!!! danger Don't Override Instance Variables 
Child class already has the variable, which can lead to problems
!!!

---
### Override Example

#### Superclass

```java
public class Person {

    protected String name;
    
    public Person(String n) {
        this.name = n;
    }
    
    public String toString() {
        return "Hello, my name is " + name;
    }
```
#### Subclass

```java
public class Student extends Person {
    protected int yr;
    
    public Student(String name, int year) {
        super(name);
        this.yr = year;
    }
    
    public Student(String name) {
        this(name, -1);
    }
    
    @Override
    public String toString() {
        return "Yo, my name is " + name;
    }
```

---

## Object Class 
Object Class 
~ Every class has Object as a superclass. All objects, including arrays, implement the methods of this class.


- The Object class contains:
  - equals()
  - toString()
  - clone()
  - [Other Methods](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)
- Overriding equals()
  - Check if object is not null
  - Check for reference equality (==)
  - Check if the other object is *instanceof* class
  - Cast other object to intended class (guaranteed to work after *instanceof* check) 


### Example of Overriding Object Class
```java
public class GrizzlyBear {
    protected String name;

    public GrizzlyBear(String name) {
        this.name = name;
    }
```

#### equals()
```java
  @Override
public boolean equals(Object other) {
    if (null == other) {
      return false; }
    if (this == other) {
      return true;
    }
    if (!(other instanceof GrizzlyBear)) {
      return false;
    }
    GrizzlyBear that = (GrizzlyBear) other;
    return this.name.equals(that);
```

#### toString()
```java
    @Override
    public String toString() {
        return name;
    }
```

---

## Glossary

Child Class
~ class that "extends" a super class
~ sub class
~ derived class

Inheritance
~ process of deriving a new class from an existing one.

Object Class
~ Every class has Object as a superclass. All objects, including arrays, implement the methods of this class.

Override
~ provide a new implementation for a method in the subclass.

Parent Class
~ super class
~ base class

super
~ access to parents members 
~ "this()" for parent class


