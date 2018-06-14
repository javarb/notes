# SOFTWARE ENGINEERING IN JAVA

## Session 3 (11/06/2018)
- Github pull request comments addressing
- Ways to make the code cleaner and shorter
	- Fixing indentation
	- Inverting if statements
	- Returning inside if statements 
	- Mantain methods shorter possible	
- Used `ArrayList` to keep the contents of the opened file
- Manual importing of libraries (jars files)

### Notes:

#### Making code clean and shorter
Roger created a branch called Javier in his GitHub, there he made a pull request addressing to me several precision in regards to clean code and good practices. In this session we were reviewing some of the Roger's comments on that github's pull request and other subjects arised while we were reviewing my code:

##### Fixing indentation

In Java generally indentation is of 4 spaces or 1 tab. 

As I had my indentation mixed, (and always we need it), we can use `Alt+Shift+L` or right mouse click over the file (in the left files list of project) and click on `reformat code`. In general is a good practice to do it frecuently.

##### Inverting if statements.

Whe use of nested `if-else` statements produce indentation in our code and makes it harder to follow. In order to solve this we can invert our if-else statements hitting `Alt+Enter` over the `if` word and pressin `Enter` or `Click` over `Invert the 'if' condition`

This inverting utility also denies the `if` statement if it's truly and truly if it's falsy. 

Example, inverting the following condition:

```java
		if (args[0].equals(DataBasicCommands.INSERT.toString())) {
			validateInsert(args);
		}
```

Results in:
```java
		if (!args[0].equals(DataBasicCommands.INSERT.toString())) {

		} else {
			validateInsert(args);
		}
```
And vice versa

##### Returning inside if statements 

In the `validateInput` method of `InputProcessor` Class, we used `return` statements inside the `if` statements (or other methods called from there) in order to avoid use of nested `else if` conditions and make code shorter and nicer to read.

Finally, that method finished with two if statements:
- First `if` for `help` command 
- Secound `if` for the `insert` command. 

In this way, the `query` command option stands as default outside of any `if` and, implicitly, of their `return` instructions. So `query` command is executed when no arguments are provided:
```java
		// Check commands
        if (args[0].equals(DataBasicCommands.HELP.toString())) {  
            help();
            return;
        }
        if (args[0].equals(DataBasicCommands.INSERT.toString())) {
            validateInsert(args);
        }

        // Default, make a query
        System.out.println("Querying...");
        return;  //finish the method execution
```

##### Mantain methods shorter possible.

Is a general rule and good practice to keep short methods length 20 lines of code could work but a good code recommendation from Roger is 6 lines of code maximun per method.

In order to make methods shorter, we can delegate part to our code to create new methods. This can be done in IntelliJ IDEA with `Ctrl+Alt+M` or selecting desired text, right mouse click over it and click in `Refactor/Extract/Method` option. After choose a method name and parameters.

For the `Main` method the recommended is to have just 1 line length So this: 
```java
InputProcessor inputProcessor = new InputProcessor();
inputProcessor.validateInput(args);
```
Could be written as:
```java
new InputProcessor().validateInput(args);
```
Indeed in the future this will be:
```java
new Application().start(args);
```

#### Used `ArrayList` to keep the contents of the opened file

For [Reading files] using a `Stream`. After we're saving each of this lines into an [ArrayList].

```java
    private List<String> getLines(String fileName) throws IOException {
        Stream<String> linesStream = Files.lines(Paths.get(fileName));
        List<String> lines = new ArrayList<>();
        System.out.println("<!-----Read all lines as a Stream-----!>");
        linesStream.forEach(s -> lines.add(s));
        linesStream.close();
        return lines;
    }
```

`ArrayList` is an implementation of `List`, however the type of the `lines` varible and also the `getLines` method (and returned value) is `List` not `ArrayList`. This is specially important, since this allows us to implement different kind of lists -if desired- and not have to change all the code in our application (methods, varibles, etc.) for this reason.

For other side, when we declare the variable of type `List` it's not neccesary to write the datatype in the implemented list `ArrayList`. So we can write:
```jav
        List<String> lines = new ArrayList<>();
```
Instead of:
```java
       List<String> lines = new ArrayList<String>();
```

### Resources:
- [Steps for adding external jars in IntelliJ IDEA](https://stackoverflow.com/a/1051705)
- [Set input arguments in IntelliJ IDEA](https://stackoverflow.com/a/11159341)
- [Command-Line Arguments](https://docs.oracle.com/javase/tutorial/essential/environment/cmdLineArgs.html)
- [Comparing Strings in Java](https://stackoverflow.com/a/513839)
- [Comparing Strings with 'enum' values](https://stackoverflow.com/a/9858135)
- [Printing all 'enum' values](https://stackoverflow.com/a/14413618)
- [Enums values in lowercase] https://stackoverflow.com/a/19894176
- [Bolding text](https://stackoverflow.com/a/29109958) and [ANSI escape reference](http://ascii-table.com/ansi-escape-sequences.php)
- [Reading files]
- [ArrayList]
- [JSON manipulation library 'jackson'](http://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-core/2.9.5/)

[Reading files]: https://examples.javacodegeeks.com/core-java/java-8-read-file-line-line-example/
[ArrayList]: https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html

### Homework

- ~~To apply all the comments and suggestions in Guthub pull's resquest before merge with Javier branch in Roger's Github~~
- To use JSON validator library 