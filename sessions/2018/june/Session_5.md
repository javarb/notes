# SOFTWARE ENGINEERING IN JAVA

## Session 5 (25/06/2018) (*working on*)

- GitHub practice - pull request
- Working with exceptions
- Java primitives and datatype objects
- Difference between `==` and `equals`

### Notes:

**Pull requests**
When making a pull request is util to use comments that advice the tasks or steps pending or in process. Also is very util to make a brief description the things are being covered in order to provide enough fedback to the interested parties.

Roger was talking me about the possibility to adapt [CI/CD][1] process to the development pipeline of our code. He showed to me an example of CI for one of his repositories using [Travis](https://travis-ci.org/kinbiko/bugsnag-maven-plugin)

We were talking about possibility to include these processes into our classes and the possibility to deploy into a real cloud hosted application using kubernetes. Roger was talking me also about [Zeit][4] [Cloud Broker][5] and recommended to me the reading about microservices, specially the book [***Building Microservices**, Designing Fine-Grained Systems*][6].

**Exceptions**

Java uses `checked exceptions` in several methods in order to avoid programmers omissions of certain conditions for handle adequately error events. For example the fact to open a file needs an error handling when the path doesn't exists. So if a error handling isn't configured for Java's open file method, the program will not be compiled.

In Java exists two ways to handle exceptions: *Catch* and *Throws* clause. The *Catch* clause is prefereable since if we use *Throws* clause in a method, this will be needed to use it in every method and classes related with the current method.

In the following example code, the class `Application` is implementing the interface `ExceptionThrower` which has defined the method `void e() throws Exception;`. We can see there several nested methods and how the last called method is the implementation of interface's method with the *Throws* clause. Therefore, all the calling methods, even the main method, have to add that same *Throws* clause:

```java
package exceptions;

class Application implements ExceptionThrower{

    public static void main(String[] args) throws Exception {
        new Application().run();
    }

    private void run() throws Exception {
        a();
    }

    private void a() throws Exception {
        b();
    }

    private void b() throws Exception { 
        c(); 
    }

    private void c() throws Exception {
        d();
    }

    private void d() throws Exception {
        e();
    }

    public void e() throws Exception {
        throw new Exception();
    }

}

interface ExceptionThrower{
    void e() throws Exception;
}
```

That is very inconvenient, and is prefereable to use a *Catch* clause:

```java
package exceptions;

class Application implements ExceptionThrower{

    public static void main(String[] args) {
        new Application().run();
    }

    private void run() {
        a();
    }

    private void a() {
        b();
    }

    private void b() { 
        c(); 
    }

    private void c() {
        d();
    }

    private void d() {
        e();
    }

    public void e() {
        try {
            throw new Exception();
        } catch (Exception e) {

        }
    }

}

interface ExceptionThrower{
    void e() throws Exception;
}
```

### Resources:

- [What is CI/CD? Continuous integration and continuous delivery explained][1]
- [Continuous integration vs. continuous delivery vs. continuous deployment][2]
- [What Is CI/CD?][3]
- [Book: Building Microservices][6]
- [Zeit Cloud Broker][4]
- [Cloud broker][5]


[1]: https://www.infoworld.com/article/3271126/application-development/what-is-cicd-continuous-integration-and-continuous-delivery-explained.html
[2]: https://www.atlassian.com/continuous-delivery/ci-vs-ci-vs-cd
[3]: https://dzone.com/articles/what-is-cicd
[4]: https://zeit.co/
[5]: https://en.wikipedia.org/wiki/Cloud_broker
[6]: http://shop.oreilly.com/product/0636920033158.do

### TODO:

- [ ] Databasic: Make principal Application Class and move all main stuff there.