# SOFTWARE ENGINEERING IN JAVA

## Session 22 (15/01/2019)

- Java Memory Handling
- Changes in Logger implementation
- Sprint work-flow in GitHub project for estimate effort
- Linter
- Microservices resources
- Git advices

### Notes

#### Java memory

![Java memory](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/jvm-3.jpg "Java memory")

Java uses their JVM to distribute its own memory use.

In `Heap` is the zone where values of data are. References are in `JVM Language Stacks`. So for example for the declaration `String foo = "bar"`, `foo` reference exists in the `Stack` and `"bar"` exists in the `Heap`.

`PC Registers` is where CPU instructions are stored. `Native Method Stack` is where the methods that Java has built in are, and `Method Area` is self descriptive.

`Class Loader` is where the compiled classes are found when the program is executed. As an example of this, I could to compile a program, and after it, proceed to remove the `.class` file from the `Class Loader` corresponding folder, after that, if I try to run the program will not do it, because the code isn't where is supossed to be, but if I compile again the code, this will not fail and work since the class is recreated into the `Class Loader` zone.

#### Changes in Logger implementation

Several improvements were made to the DefaultLogger class:

```java
@Component
public class DefaultLogger implements Logger {
    private final String ip;

    DefaultLogger () {
        InetAddress inetAddress;

        try {
            inetAddress = InetAddress.getLocalHost();
        } catch (UnknownHostException e) {
            inetAddress = null;
        }

        if (inetAddress != null){
            ip = inetAddress.toString();
        } else {
            ip = "";
        }
    }

    @Override
    public void log(String message) {
        Timestamp timestamp = new Timestamp(System.currentTimeMillis());
        long threadId = Thread.currentThread().getId();

        message = timestamp + "  INFO [" + threadId + "] " + ip + ": " + message;
        System.out.println(message);
    }
}
```

A very important point here is that the system is asking for the IP address (`InetAddress.getLocalHost()`) in the constructor, so this is executed just once and the value is cached and used wherever is needed and not consulted each time when the method `log()` is called. Also, `null` inspection was made when the IP address of the system running cannot be loaded for some reason, avoiding to be using methods of `null` objects and receive `Null Pointer` exceptions

By other side, `threads` values cannot be cached and they need to be consulted for each `request` made.  So we find out which thread is running the log call for each invocation of `log(String)`  method.

**NOTE:** Java application is a single process that have many threads. Different threads handle concurrent requests, but because threads aren't cheap to create, Java does re-use a thread, after it has completed the execution of a request.

#### Sprint work-flow in GitHub for estimate effort

In order to estimate effort in a sprint (for us is 1 week long, but usually is 2 weeks), a number between 1 and 34 must be assigned to each task by using Fibonacci numbers:

- 1,2,3,5,8,13,21,34

Still the definition of this number is something subjective, eventually becomes consistent because is groupal and advances according to the grade of difficulty of the tasks. So the idea of hardness is not the same for a work team of experts than for junior programmers, but anyway the level chosen in the team will be preserved for them and advance through the time.

That said, is important to mention that the most important here is not to measure times, but to be consistent, it means that if in the current week I made 13 points the most important is that I preserve my level of work in the following weeks becoming eventually better not worst.

There are some rules:

- Each task have a number of required effort

  **Note:**  We also established the convention to assign a effort number writing it at the begging of the task title using square brackets `[]` (still It isn't a hard rule).

- Not more than 1 ticket in progress column at the time

- The number of points in the current sprint (summing up all the tasks numbers in the sprint) shouldn't be lower than the **completed** effort in the last sprint, must be more. The reason for this is just so that we don't accidentally underestimate how much work we can do and end up taking longer to complete work that could have been done faster with sufficient quality (read up on the [Parkinson's law][12]).

  **Note:** As we're calibrating we could have been estimated our effort bad and so we readjust but in the long time this becomes some good indicator.

#### Linter

It's a tool that allow us to write better code by bringing up to the programmer warning messages whatever something is not being wrote according to the best programming principles and practices.  An example of use can be seen [here][4].

#### Microservices resources

Micro-services architecture rely on technologies such as [REST (the most common) or RPC][7] in order to communicate different components of an application. Some of the most widely used are the following:

- [gRPC][8]. Synchronous messaging. Has a lot of things to learn.
- [Apache kafka][9]. Asynchronous. Harder to use but best possibilities at big scale
- [RabbitMQ][10].  Asynchronous. Easier to use, the best option to begin with.

#### Advices in GitHub

Roger was giving to me some examples of things that can happen in GitHub and not be what we were wanting to do. 

He said me that for example once, when he was making a commit in his current company, he referenced an issue of a open source software they were using in his team. When the commit was made, the commit appeared into the open source project issue, which wasn't desired. [See here][11]. 

That happened because he wrote the link to the issue inside his commit message. So the recommendation was maybe use anoter way to write the link as for example: "Look at issue number # at http://url"

Other thing that happened to him in GitHub was he wrote in a commit message saying that was closing an issue, and so the issue was automatically closed, but that was not the intended because it could be saw as something a little rude.

So those are things to have present with GitHub.

### Homework

Make the sprint scheduled work

### Resources

- [Timestamp][1]
- [Get IP info][2]
- [Get thread ID][3]
- [JS Lint][5]
- [REST, RPC, and Brokered Messaging][7]
- [gRPC][8]
- [Apache kafka][9]
- [RabbitMQ][10] 
- [Neofetch - Command-line system information tool][6]
- [Parkinson's law][12]


[1]: https://www.mkyong.com/java/how-to-get-current-timestamps-in-java/
[2]: https://crunchify.com/how-to-get-server-ip-address-and-hostname-in-java/
[3]: https://stackoverflow.com/questions/3294293/how-to-get-thread-id-from-a-thread-pool
[4]: https://github.com/JStonham/budjen/pull/33/files
[5]: https://eslint.org/
[6]: https://github.com/dylanaraps/neofetch
[7]: https://medium.com/@natemurthy/rest-rpc-and-brokered-messaging-b775aeb0db3
[8]: https://grpc.io/
[9]: https://kafka.apache.org/
[10]: https://www.rabbitmq.com
[11]: https://github.com/satori/go.uuid/issues/66
[12]: https://en.wikipedia.org/wiki/Parkinson%27s_law