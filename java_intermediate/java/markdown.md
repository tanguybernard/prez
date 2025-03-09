# Java Intermediate

Tanguy Bernard

-----

<div style="color: #dc3f00; font-size: xxx-large">
Input - Output
</div>

---

## Definition

Java's Input/Output (I/O) system is used for managing data flow between a program and external sources or destinations, such as files, the console, or network sockets.

---

## Concepts

- Input: Reading data from a source (e.g., file, keyboard, network).
- Output: Writing data to a destination (e.g., file, screen, network).
- Streams: Abstract representations of data flow, used for reading and writing data sequentially.

---


### Schema


![Input,Output](./java/assets/input-output.jpg)


<div style="font-size:small;color: #7d889a">
source: https://dh-cologne.github.io/java-wegweiser/articles/IO.html
</div>

---

### Scanner


```java
import java.util.Scanner;

public class KeyboardInputExample {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Enter your name: ");
    String name = scanner.nextLine();
    System.out.println("Hello, " + name + "!");
    
  }
}
```

---

## Api

Java provides a comprehensive API for I/O operations through the java.io package.

And java.nio offering non-blocking I/O capabilities.


---

### File Input and Output

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

###  Stream

---
### Byte Streams for Binary Files

Example: Copying a Binary File


```java
import java.io.*;

public class FileCopyExample {
    public static void main(String[] args) {
        try (FileInputStream input = new FileInputStream("source.jpg");
             FileOutputStream output = new FileOutputStream("destination.jpg")) {
             
            byte[] buffer = new byte[1024];
            int bytesRead;
            while ((bytesRead = input.read(buffer)) != -1) {
                output.write(buffer, 0, bytesRead);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```


---

### Using java.nio

```java
import java.nio.file.*;
import java.io.IOException;

public class NioExample {
    public static void main(String[] args) {
        try {
            String content = Files.readString(Path.of("example.txt"));
            System.out.println(content);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

-----

<div style="color: #dc3f00; font-size: xxx-large">
Serialization
</div>

--- 

### Definition

Serialization is the conversion of the state of an object into a byte stream; deserialization does the opposite.

---

### Serializable

```java
public class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    static String country = "ITALY";
    private int age;
    private String name;
    transient int height;

    // getters and setters
}
```

---

### Serialize

```java
Person person = new Person();
person.setAge(20);
person.setName("Joe");

FileOutputStream fileOutputStream
  = new FileOutputStream("yourfile.txt");
ObjectOutputStream objectOutputStream 
  = new ObjectOutputStream(fileOutputStream);
objectOutputStream.writeObject(person);
objectOutputStream.flush();
objectOutputStream.close();
```

---

### Deserialize

```java    
FileInputStream fileInputStream
  = new FileInputStream("yourfile.txt");
ObjectInputStream objectInputStream
  = new ObjectInputStream(fileInputStream);
Person p2 = (Person) objectInputStream.readObject();
objectInputStream.close(); 
```

---

### With Library like Jackson or Gson

Convert objects to JSON and vice versa

### Deserialize

```java    
public class JacksonSerializationExample {
    public static void main(String[] args) {
        // Création d'un objet Student
        Student student = new Student("Bob", 25, "S98765");

        // ObjectMapper de Jackson
        ObjectMapper objectMapper = new ObjectMapper();

        try {
            // Sérialisation : Objet vers JSON
            String jsonString = objectMapper.writeValueAsString(student);
            System.out.println("JSON Serialized: " + jsonString);

            // Désérialisation : JSON vers Objet
            Student deserializedStudent = objectMapper.readValue(jsonString, Student.class);
            System.out.println("Deserialized Object: " + deserializedStudent);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

-----

<div style="color: #dc3f00; font-size: xxx-large">
Collection
</div>

---

-----

<div style="color: #dc3f00; font-size: xxx-large">
Generics
</div>

---

### Introduction


Generics in Java allow developers to write flexible, type-safe code by parameterizing classes, methods, and interfaces with types. This feature enhances compile-time type checking, eliminates the need for explicit casting, and reduces runtime errors.

---

## Generic Classes

```java
// Generic Pair class to hold two related objects
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }

    @Override
    public String toString() {
        return "(" + key + ", " + value + ")";
    }
}
```

---

```java
public class GenericClassExample {
    public static void main(String[] args) {
        // Create a Pair of Integer and String
        Pair<Integer, String> pair1 = new Pair<>(1, "One");
        System.out.println(pair1);

        // Create a Pair of String and Double
        Pair<String, Double> pair2 = new Pair<>("Pi", 3.14);
        System.out.println(pair2);
    }
}
```

---

### Generic Methods

```java
public class GenericMethods {
    public static  void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        Double[] doubleArray = {1.1, 2.2, 3.3, 4.4, 5.5};
        String[] stringArray = {"Hello", "Generics", "in", "Java"};

        System.out.print("Integer Array: ");
        printArray(intArray);

        System.out.print("Double Array: ");
        printArray(doubleArray);

        System.out.print("String Array: ");
        printArray(stringArray);
    }
}
```

---

### Bounded Type Parameters

```java
public class NumberOperations<T extends Number> {
    private T[] numbers;

    public NumberOperations(T[] numbers) {
        this.numbers = numbers;
    }

    public double getAverage() {
        double sum = 0.0;
        for (T number : numbers) {
            sum += number.doubleValue();
        }
        return sum / numbers.length;
    }

    public static void main(String[] args) {
        Integer[] integers = {1, 2, 3, 4, 5};
        NumberOperations<Integer> intOps = new NumberOperations<>(integers);
        System.out.println("Average of integers: " + intOps.getAverage());

        Double[] doubles = {1.1, 2.2, 3.3, 4.4, 5.5};
        NumberOperations<Double> doubleOps = new NumberOperations<>(doubles);
        System.out.println("Average of doubles: " + doubleOps.getAverage());
    }
}
```

---

### Wildcard Example with Upper Bound _(<? extends T>)_

```java
import java.util.ArrayList;
import java.util.List;

class Animal {
    void sound() {
        System.out.println("Some generic animal sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark!");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Meow!");
    }
}

public class WildcardUpperBoundExample {
    public static void printAnimalSounds(List<? extends Animal> animals) {
        for (Animal animal : animals) {
            animal.sound(); // Safe to call because all elements are at least of type Animal
        }
    }

    public static void main(String[] args) {
        List<Dog> dogs = new ArrayList<>();
        dogs.add(new Dog());
        dogs.add(new Dog());

        List<Cat> cats = new ArrayList<>();
        cats.add(new Cat());
        cats.add(new Cat());

        System.out.println("Dog sounds:");
        printAnimalSounds(dogs);

        System.out.println("Cat sounds:");
        printAnimalSounds(cats);
    }
}

```


-----

<div style="color: #dc3f00; font-size: xxx-large">
Regex
</div>

---




## Conclusion 


- Échangez les dépenses initiales contre des dépenses variables.
- Bénéficiez d'économies d'échelle massives.
- Arrêtez de deviner les capacitées.
- Augmentez la vitesse et l'agilité.
- Arrêtez de dépenser de l'argent pour faire fonctionner et entretenir des centres de données.
- Devenez mondial en quelques minutes.

