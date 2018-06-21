# SOFTWARE ENGINEERING IN JAVA

## Session 4 (19/06/2018)

- Access modifiers
- Java packages
- Inheritance
	- Interfaces

### Notes:

#### Access modifiers

Access modifiers allows restrict in more or less measure the access to resources. The following chart describes the access scopes:

|              | Class | Package | Subclass | Subclass | World  |
|--------------|-------|---------|----------|----------|--------|
|*public*      |   +   |    +    |    +     |     +    |   +    |
|*protected*   |   +   |    +    |    +     |     +    |        |
|*no modifier* |   +   |    +    |    +     |          |    	|
|*private*     |   +   |         |          |          |    	|

More information in the from the [Java control access] documentation and this [stackOverflow answer][1].

In general this corresponds with the [Law of Demeter](https://en.wikipedia.org/wiki/Law_of_Demeter) (only talk with classes related with you) over the following elements:

- Classes 
- Methods
- Fields
- Enums
- Interfaces

What is suggested is always to use this *Access Modifiers* in order from above to below. So, depending on the needs, if this isn't possible to use the more restrictive wich is `private`, then use the next `nothing`, and doing in the same way still reach the last `public` wich is the most permisive and of common use:

- private
- nothing
- protected
- public

As mentioned, this depends on the needs, thus if we begin declarating a `Class` as `private` but we need to use it from another package, we'll need to make it `public`.

#### Java packages

Java packages allows to group similar code in a way be easy to use and import from another `Classes`. This allows to group and manage code easily, overall for big projects with a lot of files. For more information see the [Java packages] definition.

Still packages are similar to namespaces and modules in other languages, they have some differences. One of them is that packages names are commonly set using the [rDNS](https://en.wikipedia.org/wiki/Reverse_DNS_lookup) hostname of the application. For example:

- `com.kinbiko.bugsnagmavenplugin.build`
- `co.org.osso.databasic`

When we group classes into packages, is needed to consider that all classes inside same package can use each other methods directly, but if they are calling classes inside other packages, is needed to import them:

```java
import co.org.osso.databasic.query.Query;
```

#### Inheritance

There exists two kinds of inheritance *Interfaces* and *Abstract Classes*.

##### Iterfaces

Interfaces define a kind of template or schema we can use to just define functionalities (methods) of a class. However, interfaces cannot implement any method, so just define it.

We were working with a shapes example for the use of interfaces. So we create a new package called `inheritance` (this wasn't using rDNS convention)

Thereby, the `Shape` interface was created inside `ìnheritance` package and defined as follows:

```java
package inheritance;

interface Shape{

    double area();
    double circumference();

}
```

After were created 2 classes: `Square.java` and `Circle.java` for implement (inherit) `Shape` interface and set methods to calculate area and circumference (perimeter).

After, that implementations of `Shape` interface could be instantiated and used in `Main` class:

```java
Square square = new Square(10);
System.out.println("Square area = " + square.area());
System.out.println("Square circumference = " + square.circumference());

```

But an useful improvement was made to that code using the characteristics of interfaces: 

A method called `reportShape` was created. That method receives a `Shape` as argument and prints to console the returning value of the two methods defined in the interface: `area()` and `circumference()`. I this way, when the call to that method is made, a `Circle` and a `Square` object are passed in order to print the results according what object was passed as argument. This works because both objects Square and Circle are using the same interface `Shape` so we can use this as base inside the method. Following the code:

```java
package inheritance;

public class Main {

    //    Alt enter and run this (when there are several main)
    public static void main(String[] args) {

        reportShape(new Square(10));
        reportShape(new Circle(1));
    }

    private static void reportShape(Shape shape) {
        System.out.println("area = " + shape.area());
        System.out.println("circumference = " + shape.circumference());
    }

}
```

Interfaces are widely used, even in the real world where we can found several examples as a keyboard, the hands, the eyes, etc.

In programming, an use case for interfaces is a database repository where it's possible to switch between DBMS easily because the interface, then each class implementation have a particular implementation for the use of a specific DBMS.

Another example are the APIs (Application Programming Interfaces) that show a base layer to use, then we use it indifferently of the underlying code.

Use of interfaces allows to not affect programs when changes arise inside implementations. However, the only way an interface can affect it is if the interface definition changes. Indeed this is the reason for crashes in Operating Systems.

#### Other notes

To print a variable defined in low level (array of bytes) we need to build a new String
```java
byte[] jsonData = Files.readAllBytes(Paths.get(jsonFile));
System.out.println("jsonData = " + new String(jsonData));            

```

### Resources:
 - [Java control access] 
 - [StackOverflow answer][1] about control access
 - [Java packages]
 
[Java control access]: https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html
[Java packages]: https://docs.oracle.com/javase/tutorial/java/package/packages.html
[1]: https://stackoverflow.com/a/215505

### TODO
- Review Abstract classes
- Work more with exceptions. Make own exception
- Review answers to these interview questions:
 	- What is the difference between the abstract class and a interface and when you would to use them?
 	- What is the difference between checked and uncheck exceptions?
