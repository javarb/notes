# SOFTWARE ENGINEERING IN JAVA

## Session 22 (15/01/2019)

- Java Memory Handling
- Fixing Logger implmeentation
- Spring workflow in github for estimate effort
- Lint checker
- Microservices resources

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
1 to 30 using fibonacci numbers is subjective but eventually becomes more constant because is groupal and advance accordig to the
difficulty grade of the tasks (experts the hard things to do aren't the same that for junior programmers)

Rule: Not more tahn 1 ticket in progress at the time
the number of the added effor (each task have one) not must be less than the last one, must be more or as we are calibrating we could have been estimated our effort bad and so we reajust but in the long time this becomes some good indicator

https://slack-redir.net/link?url=https%3A%2F%2Fkanbanize.com%2Fblog%2Fwp-content%2Fuploads%2F2014%2F07%2FStandard_deviation_diagram-1024x725.png


Example of Roger when he referenced a issue in an open source software to his team  and the reference appeared into that issue, which wasn't desired. https://github.com/satori/go.uuid/issues/66

this was because he wrote the link to the issue inside his commit message. So recommendation is maybe use anoter way to write the link as look at 66 at http://url

Other thing that happened to him in GH was he wrote in a issuw closing this issue and so the issue was automatically closed but was something that can be saw as rude, so is something to have present with GH.


#### Lint checker

Lint checket was introduced. An example of use can be seen at https://github.com/JStonham/budjen/pull/33/files. for JS https://eslint.org/

#### Microservices resources

https://grpc.io/ a lot to learn sync
https://kafka.apache.org/ harder best possibilities async
https://www.rabbitmq.com/#getstarted  easier async

### Homework

To do what was anotated for the spring

### Resources

tip neofech for bring the computer specifications

- [Timestamp][1]
- [Get IP info][2]
- [Get thread ID][3]

[1]: https://www.mkyong.com/java/how-to-get-current-timestamps-in-java/
[2]: https://crunchify.com/how-to-get-server-ip-address-and-hostname-in-java/
[3]: https://stackoverflow.com/questions/3294293/how-to-get-thread-id-from-a-thread-pool
