# BGX-Singlet
43 44 45 BGX-Singlet/Connect.java BGX-Singlet/Config.java BGX-Singlet Main.java 76 77 77  

Cont. from 8.6 Initializing blocks [42.BHF-StatBlocks](https://github.com/Java-PJATK/42.BHF-StatBlocks)  

## 8.7 Singleton classes  

Very often we encounter the situation when we have a class of which at most one object should ever be created; such objects are called **singletons**.  

There are at least two approaches to produce such objects. If the object in question is expensive to create and it is possible that it will not be needed at all, we can use lazy evaluation approache:

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
