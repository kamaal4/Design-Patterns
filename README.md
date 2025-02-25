# Design-Patterns
Design patterns are reusable solutions to common problems that arise during software development. They are categorized into **creational**, **structural**, and **behavioral** patterns. Here are some examples of design patterns used in Android development with Kotlin:

## Creational Design Patterns

These patterns deal with object creation mechanisms.

### 1. **Singleton Pattern**
   - **Purpose**: Ensures a class has only one instance and provides a global point of access to it.
   - **Example in Android**: Useful for managing shared resources like a configuration manager or logging service.
   - **Kotlin Implementation**:
     ```kotlin
     object Singleton {
         fun doSomething() {
             println("Singleton instance doing something")
         }
     }
     ```

### 2. **Builder Pattern**
   - **Purpose**: Separates the construction of a complex object from its representation.
   - **Example in Android**: Useful for building complex UI components with many optional parameters.
   - **Kotlin Implementation**:
     ```kotlin
     class Product private constructor(
         val name: String,
         val price: Double
     ) {
         class Builder {
             private var name: String = ""
             private var price: Double = 0.0

             fun setName(name: String) = apply { this.name = name }
             fun setPrice(price: Double) = apply { this.price = price }
             fun build() = Product(name, price)
         }
     }

     // Usage
     val product = Product.Builder()
         .setName("Example Product")
         .setPrice(19.99)
         .build()
     ```

### 3. **Factory Method Pattern**
   - **Purpose**: Provides a way to create objects without specifying the exact class of object that will be created.
   - **Example in Android**: Useful for creating different types of fragments or adapters based on conditions.
   - **Kotlin Implementation**:
     ```kotlin
     abstract class FragmentFactory {
         abstract fun createFragment(): Fragment
     }

     class HomeFragmentFactory : FragmentFactory() {
         override fun createFragment(): Fragment = HomeFragment()
     }

     class SettingsFragmentFactory : FragmentFactory() {
         override fun createFragment(): Fragment = SettingsFragment()
     }
     ```

## Structural Design Patterns

These patterns deal with the composition of objects.

### 1. **Adapter Pattern**
   - **Purpose**: Allows two incompatible objects to work together by converting the interface of one object into an interface expected by the clients.
   - **Example in Android**: Useful for integrating third-party libraries with different interfaces.
   - **Kotlin Implementation**:
     ```kotlin
     interface Target {
         fun request()
     }

     class Adaptee {
         fun specificRequest() {
             println("Specific request")
         }
     }

     class Adapter(private val adaptee: Adaptee) : Target {
         override fun request() {
             adaptee.specificRequest()
         }
     }
     ```

### 2. **Facade Pattern**
   - **Purpose**: Provides a simplified interface to a complex system of classes, library, or framework.
   - **Example in Android**: Useful for simplifying interactions with complex subsystems like network requests.
   - **Kotlin Implementation**:
     ```kotlin
     class NetworkFacade {
         fun fetchData(url: String) {
             // Simplified interface to handle complex network operations
             println("Fetching data from $url")
         }
     }
     ```

## Behavioral Design Patterns

These patterns deal with interactions between objects.

### 1. **Observer Pattern**
   - **Purpose**: Defines a subscription mechanism that allows objects to be notified of changes to other objects without having a direct reference to one another.
   - **Example in Android**: Useful for updating UI components when data changes, often used with LiveData or Kotlin Flows.
   - **Kotlin Implementation**:
     ```kotlin
     class Subject {
         private val observers = mutableListOf()

         fun registerObserver(observer: Observer) {
             observers.add(observer)
         }

         fun notifyObservers(data: String) {
             observers.forEach { it.update(data) }
         }
     }

     interface Observer {
         fun update(data: String)
     }

     class ConcreteObserver : Observer {
         override fun update(data: String) {
             println("Received update: $data")
         }
     }
     ```

### 2. **Strategy Pattern**
   - **Purpose**: Allows you to define a family of algorithms, encapsulate each one, and make them interchangeable.
   - **Example in Android**: Useful for changing the behavior of an object at runtime, such as sorting algorithms.
   - **Kotlin Implementation**:
     ```kotlin
     interface SortingStrategy {
         fun sort(data: List): List
     }

     class BubbleSortStrategy : SortingStrategy {
         override fun sort(data: List): List {
             // Implement bubble sort algorithm
             return data.sorted()
         }
     }

     class QuickSortStrategy : SortingStrategy {
         override fun sort(data: List): List {
             // Implement quick sort algorithm
             return data.sorted()
         }
     }

     class Sorter(private val strategy: SortingStrategy) {
         fun sortData(data: List): List = strategy.sort(data)
     }

     // Usage
     val sorter = Sorter(BubbleSortStrategy())
     val sortedData = sorter.sortData(listOf(5, 2, 8, 3))
     ```

These design patterns help improve the structure, maintainability, and scalability of Android applications developed with Kotlin.

Citations:
[1] https://proandroiddev.com/zero-to-hero-in-android-kotlin-creational-design-patterns-a972375c352a
[2] https://getstream.io/blog/design-patterns-and-architecture-the-android-developer-roadmap-part-4/
[3] https://blog.logrocket.com/understanding-kotlin-design-patterns/
[4] https://www.youtube.com/watch?v=aW1iR0Mmitk
[5] https://reflectoring.io/kotlin-design-patterns/
[6] https://proandroiddev.com/kotlin-design-patterns-8e152540ee2c
[7] https://github.com/dbacinski/Design-Patterns-In-Kotlin
[8] https://in-kotlin.com/design-patterns/
