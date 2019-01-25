# SOFTWARE ENGINEERING IN JAVA

## Session 22 (15/01/2019)

- Lint checker. example at https://github.com/JStonham/budjen/pull/33/files. for JS https://eslint.org/
- Microservices
https://grpc.io/ a lot to learn sync
https://kafka.apache.org/ harder best possibilities async
https://www.rabbitmq.com/#getstarted  easier async
- Java Memory ahndling
- Fixing Logger implmeentation
- Spring workflow in github for estimate effort


### Notes

#### Java memory

![Java memory](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/jvm-3.jpg "Java memory")

Java uses their JVM to distribute its own memory use in heap are valiables but pointers are in JVM langiage stacks
PC registers deals with CPU instructions Native method stack is where are the methods that Java has built in

Class loader is where the compiled classes are founded when the program is executed. I could to compile, and after remove the .class file and the program will not run because the code isn't where must to be but if I compli again this will not fail and the class is recreated

- Fixing Logger implmeentation

null inpection to avoid to be using method of null objects to avoid null pointer exception

threads cannot be cached each request have a thread application is a single process that have many threads


- Spring workflow in github for estimate effort
1 to 30 using fibonacci numbers is subjective but eventually becomes more constant because is groupal and advance accordig to the
difficulty grade of the tasks (experts the hard things to do aren't the same that for junior programmers)

Rule: Not more tahn 1 ticket in progress at the time
the number of the added effor (each task have one) not must be less than the last one, must be more or as we are calibrating we could have been estimated our effort bad and so we reajust but in the long time this becomes some good indicator

https://slack-redir.net/link?url=https%3A%2F%2Fkanbanize.com%2Fblog%2Fwp-content%2Fuploads%2F2014%2F07%2FStandard_deviation_diagram-1024x725.png


Example of Roger when he referenced a issue in an open source software to his team  and the reference appeared into that issue, which wasn't desired. https://github.com/satori/go.uuid/issues/66

this was because he wrote the link to the issue inside his commit message. So recommendation is maybe use anoter way to write the link as look at 66 at http://url

Other thing that happened to him in GH was he wrote in a issuw closing this issue and so the issue was automatically closed but was something that can be saw as rude, so is something to have present with GH.

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
