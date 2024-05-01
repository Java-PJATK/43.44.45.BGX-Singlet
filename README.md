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

Certainly! In Java, a **singleton** is a design pattern that ensures a class can have only **one instance**. Let's explore the key concepts of the singleton pattern:

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
