# SOFTWARE ENGINEERING IN JAVA

## Session 18 (27/11/2018)

- Reviewing homework
- Adding BugSnag to my API code
- Partial Git commits

### Notes

#### Reviewing my Homework

Roger was reviewing my homework and made me several suggestions that has to be addressed:

- If I go to <http://localhost:8080/api/factorial/30>, I receive the result `265252859812191058636308480000000`. But If use the frontend this is rounding the result to `2.6525285981219107e+32`. So this must also show the numbers with the same precision as in the backend.

- Verify numbers are being showed as numbers and not as strings.

#### Adding BugSnag to my API code

To add BugSnag to my code I had to follow the options described in their oficial repositories to [integrate with Java][1]. Then create am account into their website. I did under my particular name (also worked as my company name). After that, I had to specify the programming language for which they provided to me the instructions to complete and test the integration.

Basically the configurations are the following:

At the controller I injected the BugSnag class and throwed a test exception:

```java
public class CalculatorController {

    private final Calculator calculator;
    private final Bugsnag bugsnag;

    public CalculatorController(Calculator calculator, Bugsnag bugsnag) {
        this.calculator = calculator;
        this.bugsnag = bugsnag;
    }

    @GetMapping("/fibonacci/{number}")
    public List<BigInteger> getFibonacci(@PathVariable("number") Integer number){
      bugsnag.notify(new RuntimeException("Test error"));
      return calculator.getFibonacci(number);
    }
...
}
```

And I just copied the BugsnagConfig class code snippet into my IDE and the class was automatically created.  

Ehen this was done I could to visit my BugSnag desktop and see the exceptions being catched at <https://app.bugsnag.com/javier-arboleda/learning-api/errors>

Any other exception is being collected automatically by the BugSnag class and sent to their API. So it isn't needed to make additional configurations.

#### Making partial git commits

When I want to add to a specific commit just a part of the code that I have modified, the following command can be used:

$ git add -p

And this will be asking for confirmation to add specific chunks of code (I can split in more chunks if I want)

Example:

```git
$ git add -p
diff --git a/build.gradle b/build.gradle
index ad5c980..87c18ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -31,4 +31,6 @@ dependencies {
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
+
 }
Stage this hunk [y,n,q,a,d,e,?]? y

diff --git a/src/main/java/co/org/osso/api/CalculatorController.java b/src/main/java/co/org/osso/api/CalculatorController.java
index 2d2549a..a61e283 100644
--- a/src/main/java/co/org/osso/api/CalculatorController.java
+++ b/src/main/java/co/org/osso/api/CalculatorController.java
@@ -1,5 +1,6 @@
 package co.org.osso.api;

+import com.bugsnag.Bugsnag;
 import org.springframework.web.bind.annotation.RestController;
 import org.springframework.web.bind.annotation.RequestMapping;
 import org.springframework.web.bind.annotation.GetMapping;
Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? y
@@ -14,13 +15,16 @@ import java.util.List;
 public class CalculatorController {

     private final Calculator calculator;
+    private final Bugsnag bugsnag;

-    public CalculatorController(Calculator calculator) {
+    public CalculatorController(Calculator calculator, Bugsnag bugsnag) {
         this.calculator = calculator;
+        this.bugsnag = bugsnag;
     }

     @GetMapping("/fibonacci/{number}")
     public List<BigInteger> getFibonacci(@PathVariable("number") Integer number){
+        bugsnag.notify(new RuntimeException("Test error"));
         return calculator.getFibonacci(number);
     }

Stage this hunk [y,n,q,a,d,K,g,/,s,e,?]? y
```

I have to verify also if there is something else to add that has not been added:

```bash
[jaar@port-staff api]$ git status
On branch bugsnag-integration
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   build.gradle
        modified:   src/main/java/co/org/osso/api/CalculatorController.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        src/main/java/co/org/osso/api/BugsnagConfig.java

[jaar@port-staff api]$ git add .
```

#### Debugging example

Instead to be printing lot of messages to console its more useful and flexible to debug the code, this is done adding breakpoints (red circles) to the code and once the application is stopped, it can be debbuged clicking on the bug icon or mouse right click menu and 'Debug Application'.  

When the application is being debugged, the value of the variables can be saw in all moment and steps can be traced over the program execution. Also, through the mouse right click menu the option Evaluate Expression can be used to evaluate and get the ouput of the desired expression in any moment. For example: `fibonacci.size()` to obtain the size of the `List` called fibonacci.

### Homework

- Make a new branch and pull request (knowing there's not commits) for reviewing purposes of my Frontend application.
- Integrate BugSnag into my Frontend application
- Address comments to my frontend code.

### Resources

- [BugSnag Integration with Java][1]

[1]: https://github.com/bugsnag/bugsnag-java
