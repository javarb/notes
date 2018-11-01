# SOFTWARE ENGINEERING IN JAVA

## Session 15 (16/10/2018)

- Reviewing/fixing Spring API homework
- API desing concepts
- Dependency injection concepts

### Notes:

Roger was reviewing my homework solution and advicing me some modifications and improvements.

#### Reviewing/fixing Spring API homework

In certain part of the code I needed to save and incremental `id` `int` field into the object's field that was a `String`. A way to do it should be changing the type of the object's field, but a simpler way (hack) to work around it is doing `id` increment and mapping to `String` by concatenating with `""` at the moment to set into the object's field:

```java
book.setBookID(""+id++);
```

__Note__: In the final solution, the object field was changed from `String` to `Integer` (handle `null` values is convenient when answering to request to inexistents elements), since the previous mentioned hack was a workaround.

Another optimization that was spoken was about to change this kind of return conditions when using `Map` structure:

```java
public Book getBook(String id) {
    if (bookCache.get(id) != null){
        return bookCache.get(id);
    } else {
        return new Book();
    }
}
```

To use the included `getOrDefault` method that comes integrated into `Map` structure:

```java
public Book getBook(String id) {
    return bookCache.getOrDefault(id, new Book());
    }
```

#### Use of the API application

When we run the application (see note below), a Tomcat server is started on port `8080`.

__Note__: If changes has been made, the application needs to be restarted. So it's important don't use `Ctrl+Shift+F10` (or the equivalent running by mouse click action), because this will start another Tomcat server instance. Instead of that, what we need to do is go over the bottom panel, and click over the green rerun arrow (first icon on the top of the left vertical menu), or just hit `Ctrl+5` key binding.

__Note__: When we're designing [RESTful][1] interfaces, a main concept is we have to use nouns and not verbs, so `fibonacci_number` is a valid route name, while `calculate` isn't.

##### GET Maps

In order to use the API we have to access GET HTTP routes trought the browser, for example going to <http://localhost:8080/api/customer> we will receive the next HTTP response:

```json
[
{
name: "Test user 1",
customerID: 1111,
emailAddress: "test1@mail.com",
dateOfBirth: "01-01-1901"
},
{
name: "Test user 2",
customerID: 2222,
emailAddress: "test2@mail.com",
dateOfBirth: "02-02-1902"
},
{
name: "Test user 3",
customerID: 3333,
emailAddress: "test3@mail.com",
dateOfBirth: "03-03-1903"
}
]
```

Those are the hardcoded users inside our API

##### POST Maps

A little different process must be follow to create books. For that we have to use some software, for example Postman, in order to send the `HTTP POST` request:

So the request we built was:

- METHOD: `POST`
- URL: `localhost:8080/api/book`
- BODY: `raw / JSON (application/json)` with the following content:
```json
{
	"title": "Test book 1",
	"year": "1901"
}
```

Once we run this request, following response is received:
```json
{
    "bookID": 0,
    "title": "Test book 1",
    "year": "1901"
}
```

That response is showing a book with `bookID: 0` was created.

After it, in order to access by HTTP GET to see our newly created book (or any other) we can go to: <http://localhost:8080/api/book/0> replacing the last digit for the desired `bookID`. Our code is prepared to answer to any inexistent `bookID` returning a null JSON object, for example:

The request <http://localhost:8080/api/book/1000>

Returns:
```json
{
bookID: null,
title: null,
year: null
}
```

#### API desing concepts

Is possible to serve Frontend Web content in Spring:
<https://spring.io/guides/gs/serving-web-content/>
<https://www.baeldung.com/spring-request-response-body>

An example to worh with HTML inside Spring is using JSP. This is very hard to work with, is very strict and not good error tracking: https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/view.html

While this is possible to serve frontend content, the aproach of separate interests must be followed, since this allow more flexibility and portability. So instead to use a full stack application in a box, we can delegate an API to do the logic tasks while we can use whatever view enging or framework or technology we want to use/access the API.

This is not the same that microservices, is just to separate the view from the API logic.

This is neither the same that Progressive Web Apps (PWA), since in these kind of applications, the content is being loaded and served from the browser self, so even without an internet connection, the application can work and serve content that has been already downloaded and sync when a connection is available. By the other side, in the API approach, a network connection is mandatory for the correct operation of the API's and its components.

In the API approach, one of the things to have present is that APIs are decoupled from the view. So we can use and switch them between different platforms. Some usual components to achieve this approach are:

- API using some backend programming language such as Java for example.
- SPA (Single Page Application) is the frontend in which we can use JS, CSS, HTML5 or some JS framework such as React, Angular or Vue since the're some of the most popular SPA options right now.


#### Dependency injection concepts

A simplification and better practice to use dependency injection in Spring was talked about. We were changing from field injection towards constructor injection.

##### Field injection

Field injection allows to link resources, so for example in the next code snippet, a controller is asking to Spring to `@Autowire` BookService from its pool of registered services:

```java
import org.springframework.beans.factory.annotation.Autowired;

@RestController
@RequestMapping("/api/book")
public class BookController {

    @Autowired
    private BookService bookService;
    // ...
}
```

__NOTE__: Field injection is the best choise for JUnit tests.


##### Constructor injection

Other way to use our service into our controller is to create a constructor that receives the service and populate a local field.

So, once we create the constructor, we can declare `BookService` field as final (by using `@Autowired` that isn't possible). And even, we don't need anymore to use `@Autowired` annotation at all as is showed following:

```java
@RestController
@RequestMapping("/api/book")
public class BookController {

    private final BookService bookService;

    BookController(BookService bookService) {
        this.bookService = bookService;
    }

    // ...
}
```

__NOTE__: Constructor injection is the best choice to use in main code.

__NOTE__: When we declare a field as final, it cannot be modified after, thus we have quicker applications and less prone to modifications by mistake in the fields we not want. By other side, is not recommended use final keyword in classes and methods because that lead to applications that are hard to work with.

#### Testing in Spring

When we are testing services in Spring, we can built separate test files and if we are testing services that have not dependencies on Spring components we can use test in normal way without use `@Autowire` annotation (injection). For example:

```java
package co.org.osso.api;

import org.junit.Assert;
import org.junit.Test;

public class ApiApplicationBookTests {

    private BookService BookServiceTarget = new BookService();

    @Test
    public void checkBookServiceGetBookWhenNull() {
        Book book = BookServiceTarget.getBook(0);
        Assert.assertEquals(null, book.getBookID());
    }

}
```

But if we have dependencies, for example __when testing a controller__, so we must to use `@Autowire` to link dependencies and call controller's methods directly, not by hitting the URLs of HTTP methods (GET, POST, PUT, etc.) in the controller maps. For example:

```java
package co.org.osso.api;

import org.junit.Assert;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class ApiApplicationBookTests {

    private BookService BookServiceTarget = new BookService();

    @Autowired
    private BookController BookControllerTarget;

    @Test
    public void checkBookServiceGetBookWhenNull() {
        Book book = BookServiceTarget.getBook(0);
        Assert.assertEquals(null, book.getBookID());
    }

    @Test
    public void checkBookControllerGetBookEqualsTo() {
      Book book = new Book();
      book.setTitle("Book in Test");
      book.setYear("1900");
      BookControllerTarget.postBook(book);
      Assert.assertEquals("1900", BookControllerTarget.getBook(0).getYear());
    }

}
```

Something to notice in the previous example is that I had to create a new book from the test self, If I don't do so, this will return `null` even if I already have populated the in-memory array from Postman. The reason for this is that my test is running in a different memory space than the running application, just like when I'm running a Java application twice or when I when I'm using two different linux terminals. This is for temporal in-memory datasets, if I'm using a database, data will be persistent.


__NOTE__: The IntelliJ IDEA editor was claiming the next warning `private field BookControllerTarget is never assigned` in the next code line:

```java
@Autowired
private BookController BookControllerTarget;
```

This happends because the free version of the software doesn't relate what is being used through Sping, while the paid version does. So in free version, in order to solve that, we have to press `Alt+Enter` and choice the `supress unsused warning if annotated by org.springframework...Autowired` option.

This also happends with:

- Fields annotated with `@Autowired`
- Classes annotated with `@RestController`
- Methods annotated with `@*Mapping`

In the other cases, the solution is similar by ignoring those warnings.

###  Homework

Write an interesting API using what you’ve learned so far with Spring.
Write a new controller (or more than one if you want), that takes some data, does something interesting with it, and makes it accessible again from the API.
Make sure you test your classes.

__Notes from the implementation:__
- An example to send several parameters by GET request:
`http://localhost:8080/api/arithmetic?operation=div&n1=2&n2=0`

- In floating point calcules is recommended use a `delta` bigger than `0.0` because the precision of the floating point operations could vary per system. Java isn't portable in this unless we use the [`strictfp`][3] keyword, but this should limit the answer on systems with better floating point calcule capabilities.

- I was using the class name `CalculatorService` but for this application that not have much sense, since this class don't handle any data model like is handle for example for users or books wich have state information such as `year`, `age` or even `author`. Mathematical operations in this example are not handling nothing of this, just returning a result. Thus, the service class was renamed from `CalculatorService` to `Calculator`.

- I methods name, we must use the form getX or getY when we have a field called X or Y, else we can use actions names. For example `getOperationsResults()` must be renamed to `calculate()`

- we can use underscores `_` between digits of large numbers to make it easier to read, for example: `Assert.assertEquals(3_628_800, target.getFactorial(10));`.
-
- Fixing factorial integer overflow (__WIP__)

#### Key question:

Do you need to always use `@SpringBootTest` for all your spring tests? Can you do a simpler normal unit test for the classes that do the "interesting" stuff, and only use `@SpringBootTest` for the classes that need to use Spring?

#### Answer:

`@SpringBootTest` annotation is only neccesary in test classes that need work with Spring components, so if we don't need work with Spring at all, we can use simple tests, instantiating target objects directly without useing injection through `@Autowired`.

So:

- No, we don't need to always use `@SpringBootTest` for all Spring tests.

- Yes, we can do simpler normal unit test for the classes that do the "interesting" stuff, and only use `@SpringBootTest` for the classes that need to use Spring.

### Resources

- [Learn REST: A RESTful Tutorial][1]
- [Java.util.Arrays.asList() Method][2]
- [Strictfp keyword in java][3]
- [SO: What is the complexity of summing a series of n numbers?][4]
- [Measure performance of an Algorithm | The big O notation][5]
- [Factorial of a large number][6]

[1]: https://www.restapitutorial.com/
[2]: https://www.tutorialspoint.com/java/util/arrays_aslist.htm
[3]: https://www.geeksforgeeks.org/strictfp-keyword-java/
[4]: https://stackoverflow.com/questions/9252891/big-o-what-is-the-complexity-of-summing-a-series-of-n-numbers
[5]: http://toolsqa.com/data-structures/big-o-notation/
[6]: https://www.geeksforgeeks.org/factorial-large-number/
