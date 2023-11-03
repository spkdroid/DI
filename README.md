**Dependency Injection (DI)** is a fundamental concept in the Spring Framework. It is a design pattern that is used to manage the dependencies between objects, allowing for loose coupling, easier testing, and greater flexibility in building and maintaining applications. Spring provides a built-in Inversion of Control (IoC) container, which is responsible for managing and injecting dependencies into Spring-managed components.

Here's how DI works in the Spring Framework:

1. **Bean Definitions**: In Spring, objects are typically called beans. These beans are defined in a configuration file, such as an XML file or Java-based configuration, where you specify which classes should be managed by the Spring container.

2. **Container**: The Spring IoC container is responsible for creating, configuring, and managing the beans. It reads the bean definitions and instantiates the beans when they are needed.

3. **Injection**: Dependencies are injected into beans by the container. Spring supports various ways to inject dependencies:

    - **Constructor Injection**: Dependencies are provided through the constructor of the class.
    
    - **Setter Injection**: Dependencies are set using setter methods.
    
    - **Field Injection**: Dependencies are injected directly into fields.
    
    - **Method Injection**: Dependencies are passed as arguments to methods when needed.

4. **Lifecycle Management**: The Spring container manages the lifecycle of beans. It creates beans when they are needed and destroys them when they are no longer in use.

Here's a simple example of DI in Spring:

```java
// A sample service class
public class MyService {
    private MyRepository repository;

    // Constructor Injection
    public MyService(MyRepository repository) {
        this.repository = repository;
    }

    // Business logic that uses the repository
    public void doSomething() {
        repository.saveData("Some data");
    }
}

// A sample repository class
public class MyRepository {
    // Methods to save data
    public void saveData(String data) {
        // Save data to a database
    }
}
```

In this example, `MyService` relies on `MyRepository`. The dependency (`MyRepository`) is injected into `MyService` using constructor injection.

Benefits of Dependency Injection in the Spring Framework:

- **Loose Coupling**: Components are not tightly coupled to their dependencies, making it easier to change implementations.
- **Testability**: You can easily test components by providing mock or stub implementations of dependencies.
- **Configurability**: You can configure the application by swapping different implementations of dependencies at runtime.

Spring provides several ways to define and configure beans and manage dependencies, such as XML-based configuration, Java-based configuration, and annotations. It's a powerful framework for building flexible and maintainable applications.

**Step 1: Set Up Your Environment**

Ensure you have Spring Framework and a compatible IDE (e.g., Eclipse, IntelliJ IDEA) installed.

**Step 2: Create Java Classes**

Create two Java classes: `MainApp` (the entry point) and `MessageService` (the service class).

**MainApp.java:**

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainApp {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");

        MessageService service = context.getBean("messageService", MessageService.class);
        System.out.println(service.getMessage());
    }
}
```

**MessageService.java:**

```java
public class MessageService {
    private String message;

    public MessageService(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}
```

**Step 3: Create Spring Configuration (Beans.xml)**

Create a Spring configuration XML file named `Beans.xml`. This file defines the beans and their dependencies.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="messageService" class="MessageService">
        <constructor-arg value="Hello, Spring!"></constructor-arg>
    </bean>

</beans>
```

**Step 4: Run the Application**

Run the `MainApp` class, and it will load the Spring context, create a `MessageService` bean with the specified message, and then print the message.

You've just created a simple Spring application that demonstrates DI using constructor injection. This is a basic example, but it illustrates the core concept of dependency injection in the Spring Framework. You can expand on this foundation to build more complex applications with Spring.
