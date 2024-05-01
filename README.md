# BGX-Singlet
43 44 45 BGX-Singlet/Connect.java BGX-Singlet/Config.java BGX-Singlet Main.java 76 77 77  

Cont. from 8.6 Initializing blocks [42.BHF-StatBlocks](https://github.com/Java-PJATK/42.BHF-StatBlocks)  

## 8.7 Singleton classes  

Very often, we encounter situations where we have a class from which at most one object should ever be created; such objects are called **singletons**.

There are at least two approaches to produce such objects. If the object in question is expensive to create and it is possible that it will not be needed at all, we can use the lazy evaluation approach:  

## Listing 43 BGX-Singlet/Connect.java  

```java
public class Connect {

    private static Connect connection = null;

    private Connect()
    { } // private - no one can create any other object

    public static Connect getInstance() {
          // lazy evaluation, no multithreading
        if(connection == null){
            connection = new Connect();
        }
        return connection;
    }
}
```
Or, if we know that such an object almost surely will be required, one can use eager
evaluation:  

## Listing 44 BGX-Singlet/Config.java

```java
public class Config {
      // eager evaluation
    private final static Config config = new Config();

    private Config() {  // no one can create another object
        // ...
    }

    public static Config getInstance() {
        return config;
    }
}
```
## Listing 45 BGX-Singlet/Main.java

```java
public class Main {
    public static void main(String[] args) {
        Connect con1 = Connect.getInstance();
        Connect con2 = Connect.getInstance();
        if (con1 == con2) System.out.println("con1==con2");
        Config cnf1 = Config.getInstance();
        Config cnf2 = Config.getInstance();
        if (cnf1 == cnf2) System.out.println("cnf1==cnf2");
    }
}
```
and the output is  

```
con1==con2
cnf1==cnf2
```

Next 8.8 Records [46.ELR-Records](https://github.com/Java-PJATK/46.ELR-Records)  


---

MS Copilot:

[1]: https://www.geeksforgeeks.org/singleton-design-pattern-in-java/ ""
[2]: https://www.javadevjournal.com/java-design-patterns/singleton-design-pattern/ ""
[3]: https://www.programiz.com/java-programming/singleton ""
[4]: https://towardsdev.com/singleton-pattern-in-java-39651339ca1a ""
[5]: https://www.javatpoint.com/singleton-design-pattern-in-java ""

In Java, a **singleton** is a design pattern that ensures a class can have only **one instance**. Let's explore the key concepts of the singleton pattern:

1. **Private Constructor**:
   - A singleton class has a **private constructor** to prevent external instantiation.
   - This means that objects cannot be created directly from outside the class.
   - Example:
     ```java
     public class Singleton {
         private Singleton() { } // Private constructor
     }
     ```

2. **Private Instance**:
   - The class contains a **private static instance** of itself.
   - This instance is shared across all parts of the program.
   - Example:
     ```java
     public class Singleton {
         private static Singleton instance; // Private static instance
     }
     ```

3. **Static Method for Access**:
   - A **static method** provides access to the singleton instance.
   - It ensures that only one instance is created if it doesn't already exist.
   - Example:
     ```java
     public class Singleton {
         public static Singleton getInstance() {
             if (instance == null) {
                 instance = new Singleton();
             }
             return instance;
         }
     }
     ```

4. **Use Cases**:
   - **Database Connection Management**:
     - Ensuring a single database connection instance throughout the application.
     - Creating a new database connection for each request can be resource-intensive.
   - **Logger Classes**:
     - Managing a single logger instance to centralize log information.

Remember, singletons are powerful tools, but use them judiciously. They're like the **one ring** in the realm of Java programming—precious, but handle with care! 🌟

For more details and examples, check out these resources:
- [GeeksforGeeks Singleton Design Pattern](https://www.geeksforgeeks.org/singleton-design-pattern-in-java/) ¹[1]
- [Java Development Journal](https://www.javadevjournal.com/java-design-patterns/singleton-design-pattern/) ²[2]
- [Programiz](https://www.programiz.com/java-programming/singleton) ³[3]
- [Towards Dev](https://towardsdev.com/singleton-pattern-in-java-39651339ca1a) ⁴[4]
- [Javatpoint](https://www.javatpoint.com/singleton-design-pattern-in-java) ⁵[5]

Source: Conversation with Bing, 01/05/2024
(1) Singleton Design Pattern in Java - GeeksforGeeks. https://www.geeksforgeeks.org/singleton-design-pattern-in-java/.
(2) Singleton Design Pattern | Java Development Journal. https://www.javadevjournal.com/java-design-patterns/singleton-design-pattern/.
(3) Java Singleton (With Example) - Programiz. https://www.programiz.com/java-programming/singleton.
(4) Singleton Pattern in Java - Towards Dev. https://towardsdev.com/singleton-pattern-in-java-39651339ca1a.
(5) Singleton Design Patterns - Javatpoint. https://www.javatpoint.com/singleton-design-pattern-in-java.

---

## Singleton

The _**singleton pattern**_ is another well-known design pattern. It is intended to solve the design issue where only a single instance of a class is required or desired. Java provides a number of different possible ways to implement the singleton pattern. In our discussion, we will use a slightly more verbose form, which has the benefit of being very explicit in what needs to happen for a safe singleton:

```java
public class Singleton {
    private final static Singleton instance = new Singleton();
    private static boolean initialized = false;
     // Constructor
    private Singleton() {
        super();
}

private void init() {
    /* Do initialization */
}

// This method should be the only way to get a reference
// to the instance

public static synchronized Singleton getInstance() {
    if (initialized) return instance;
    instance.init();
    initialized = true;
    return instance;
  }
}
```
Java in a Nutshell

put every java code element between ticks ` ` 

The crucial point is that for the singleton pattern to be effective, it must be impossible to create more than one of them, and it must be impossible to get a reference to the object in an uninitialized state (see later in this chapter for more on this important point). To achieve this, we require a private constructor, which is only called once. In our version of Singleton, we only call the constructor when we initialize the private static variable instance. We also separate out the creation of the only Singleton object from its initialization—which occurs in the private method `init()`.

With this mechanism in place, the only way to get a reference to the lone instance of Singleton is via the static helper method, getInstance(). This method checks the flag initialized to see if the object is already in an active state. If it is, then a reference to the singleton object is returned. If not, then getInstance() calls init() to activate the object, and flicks the flag to true, so that next time a reference to the Singleton is requested, further initialization will not occur.

Finally, we also note that getInstance() is a synchronized method. See Chapter 6 for full details of what this means, and why it is necessary, but for now, know that it is present to guard against unintended consequences if Singleton is used in a multithreaded program.

> ![TIP]  
> Singleton, being one of the simplest patterns, is often overused. When used correctly, it can be a useful technique, but too many singleton classes in a program is a classic sign of badly engineered code.

The singleton pattern has some drawbacks—in particular, it can be hard to test and to separate out from other classes. It also requires care when used in mulithreaded code. Nevertheless, it is important that developers are familiar with it, and do not accidentally reinvent it. The singleton pattern is often used in configuration management, but modern code will typically use a framework (often a _dependency injection_) to provide the programmer with singletons automatically, rather than via an explicit `Singleton` (or equivalent) class.

