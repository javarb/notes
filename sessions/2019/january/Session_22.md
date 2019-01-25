# SOFTWARE ENGINEERING IN JAVA

## Session 22 (15/01/2019)

- Java Memory Handling
- Fixing Logger implmeentation
- Sprint workflow in GitHub project for estimate effort
- Lint checker
- Microservices resources
- Git advices

### Notes

#### Java memory

![Java memory](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/jvm-3.jpg "Java memory")

Java uses their JVM to distribute its own memory use.

In `Heap` is the zone where variables are. Pointers are in `JVM Language Stacks`.
`PC Registers` is where CPU instructions are stored. `Native Method Stack` is where the methods that Java has built in are, and `Method Area` is self descriptive.

`Class Loader` is where the compiled classes are found when the program is executed. As an example of this, I could to compile a program, and after it, proceed to remove the `.class` file from the `Class Loader` corresponding folder, after that, if I try to run the program will not do it, because the code isn't where is supossed to be, but if I compile again the code, this will not fail and work since the class is recreated into the `Class Loader` zone.

#### Fixing Logger implementation

Several fixes were made to the DefaultLogger class:

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

A very important point here is that the system is asking for the IP address (`InetAddress.getLocalHost()`) in the constructor, so is executed once and the value is cached and used wherever is needed and not consulted each time when the method `log()` is called. Also, `null` inspection was made when the IP address of the system running cannot be loaded for some reason, avoiding to be using methods of `null` objects and receive `Null Pointer` exceptions

By other side, `threads` values cannot be cached and they need to be consulted for each `request` made (each request is a `thread`).

**NOTE:** Java application is a single process that have many threads.

#### Spring workflow in github for estimate effort

In order to estimate effort in a sprint (cicle of 1 week), a number between 1 and 34 must be assigned to each task using fibonacci numbers:

- 1,2,3,5,8,13,21,34

Still the definition of this number is something subjective, eventually becomes constant because is groupal and advance according to the grade of difficulty of the tasks. So the idea of hardness is not the same for a work team of experts than for junior programmers, but anyway the level choosen in the team will be preserved for them and advance through the time.

That said, is important to mention that the most important here is not to measure times, but to be constant, it means that if in the current week I made 13 points the most important is that I preserve my level of work in the following weeks becoming eventually better not worst.

There is some rules:

- Each task have a number of required effort
- The assigned effort number must be written at the beggining of the task title using square brackets `[]`
- Not more than 1 ticket in progress column at the time
- The number of the added effort (summing up all the tasks numbers in the spring) not must be less than the last one, must be more. As we're calibrating we could have been estimated our effort bad and so we reajust but in the long time this becomes some good indicator.

#### Lint checker

Lint checker was introduced. An example of use can be seen [here][4]. It's a tool that allows to write better code by bringing up to the programmer warning messages whatever something is not being wrote according to the best programming principles and practices.

#### Microservices resources

Microservices architecture rely on technologies such as [REST or RPC][7] in order to comunicate different components of an application. Some of the most widely used are the following:

- [GRPC][8]. Synchronous messaging. Has a lot of things to learn.
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
- [GRPC][8]
- [Apache kafka][9]
- [RabbitMQ][10] 
- [Neofetch - Command-line system information tool][6]


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