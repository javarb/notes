# SOFTWARE ENGINEERING IN JAVA

## Session 16 (06/11/2018)

- Optimizations to Homework code

### Notes:

This session was a reviewing of the homework code, specially the part dealing with fibonacci series:

```java
public List<Integer> getFibonacci(Integer number) {
     List<Integer> fibonacci = new ArrayList<>();
    fibonacci.add(1);
    fibonacci.add(1);
     for (int i = 2; i < number; i++) {
        fibonacci.add(i, fibonacci.get(i - 1) + fibonacci.get(i - 2));
    }
     return fibonacci;
 }
```

For that code, linear time complexity `O(n)` is used, that means that the running time will increase according to the input number.

The code was upgrade to the following:

```java
List<BigInteger> fibonacci = new ArrayList<>();

public List<BigInteger> getFibonacci(Integer number) {

    if (fibonacci.size() >= number){
        System.out.println("CACHE number = " + number);
        return fibonacci.subList(0,number-1);
    }

    if (fibonacci.size() == 0) {
        fibonacci.add(BigInteger.ONE);
        fibonacci.add(BigInteger.ONE);
    }

    for (int i = 2; i < number; i++) {
       fibonacci.add(i, fibonacci.get(i - 1).add(fibonacci.get(i - 2)));
    }

    return fibonacci;

}
```
In order to improve the time complexity, when a number is given, we check if that number is less or equal than the size of our fibonnaci List. If so, that means we already have calculated that fibonnaci series, and we return the sublist still the that fibonnaci number in which case we will run on a constant `O(1)` time complexity.

Also, the definition of the `List` used to store fibonacci numbers was placed in a field and the datatype of it was changed to `BigInteger` in order to avoid the integer overflow problem. Also `BigInteger.ONE` method is used when is needed to fill list with number 1.

Other change was to use `.add()` method in repace to the `+` operator to do the addition of numbers into the bucle.

Other proposed improvement in terms of space complexity is to use the same couple of variables to overrite the values each time instead to use a `List` as can be sawn in the following fragment of `Go` code:

```go
func fibonacci() func() int {
    x, y := 0, 1
    return func() int {
        x, y = y, x + y
        return x
    }
}
```

In order to reduce the time complexity other solutions using matrices can be seen [here][1], [here][2] and [here][3].

### Resources
- [The Nth Fibonacci Number in O(log N)][1]
- [The Linear Algebra View of the Fibonacci Sequence][2]
- [Geeks for Geeks - Program for Fibonacci numbers][3]
- [Big O Cheatsheet][4]
- [Big O Notation][5]

[1]: https://kukuruku.co/post/the-nth-fibonacci-number-in-olog-n/
[2]: https://medium.com/@andrew.chamberlain/the-linear-algebra-view-of-the-fibonacci-sequence-4e81f78935a3
[3]: https://www.geeksforgeeks.org/program-for-nth-fibonacci-number
[4]: http://bigocheatsheet.com/
[5]: https://www.interviewcake.com/article/java/big-o-notation-time-and-space-complexity
