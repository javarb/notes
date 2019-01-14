# SOFTWARE ENGINEERING IN JAVA

## Session 21 (08/01/2019)

- Corrections to fibonacci algorithm.
- Implementing Logger and tests for it.

### Notes

Some improves where done to the code in fibonacci in order to make it easier to read.

#### Logger

In order to implement log capability we created the follow interface:

```java
package co.org.osso.api;

public interface Logger {
    void log(String message);
}
```

And after implement it inside a DefaultLogger class.

### Homework

For the flow activities track we're using projects and kanban method embeeded into GitHub's interface.

- Find why Travis was failing in build the Session

  **A/** this was because we were trying to use Logger inside Calculator class but Spring could not recognize this as a bean, so we had to add the `@Component` annotation to DefaultLogger Logger's implementation.

- Implement more common log components: Timestamp, IP address, Thread ID (test it). Show these in every log call


### Resources

- [Timestamp][1]
- [Get IP info][2]
- [Get thread ID][3]

[1]: https://www.mkyong.com/java/how-to-get-current-timestamps-in-java/
[2]: https://crunchify.com/how-to-get-server-ip-address-and-hostname-in-java/
[3]: https://stackoverflow.com/questions/3294293/how-to-get-thread-id-from-a-thread-pool
