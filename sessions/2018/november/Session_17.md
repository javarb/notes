# SOFTWARE ENGINEERING IN JAVA

## Session 17 (13/11/2018)

- Java API backend and JavaScript+HTML+CSS frontend Application demo

### Notes

Roger was showing me an example of an application he developed, this was the game called hangman that consists in guess a word with a maximum the tries.

The code of the Java API Backend is on <https://github.com/kinbiko/hangman> and the Frontend code is on <https://github.com/kinbiko/hangman-frontend>

#### Backend

##### Groovy

The backend application was written with a service in groovy which is a language based in Java but with several advantages such as simpler variable definition, not need of final semicolons and several utile methods such as `bytes` as is shown following:

```groovy
final String stringRepresentation = new String(new File("src/main/resources/passwords.txt").bytes)
```

In this case that piece of code is extracting the content of the passwords.txt as bytes and and placing it in a `String `` variable

Groovy is a good language to learn but is dependant on be updated with Java versions, because Java is the dominant programming language.

Other languaged based o Java are Kotlin and Scala also an example of Languaje based in another is
javaScript and Coofe

##### Domain Specific Language   

A Domain Specific Language (DSL) are small programming languages used inside an application with the purpose to execute certain focused tasks into an application, examples of it are SQL, CSS , regular expressions. Gradle scripts written with Groovy are other exampke if a DLS

### Homework
Make the fronted for the Java API calculator.

1: ### Resources


- [Domain-specific language][1]
- [Domain Specific Languages Book][2]
- [Domain Specific Languages Video][3]


1: https://martinfowler.com/books/dsl.html
2: https://martinfowler.com/dsl.html
3: https://channel9.msdn.com/blogs/charles/expert-to-expert-martin-fowler-and-chris-sells-perspectives-on-domain-specific-languages
