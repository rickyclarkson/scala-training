Lambdas
=======

Lambdas are anonymous functions.  They're coming up in Java 8, and are in most modern languages in various forms.

Here's a simple example that takes a list of names and greets everyone on it:

```scala
val names = List("John", "Juan", "Joe", "Josep")
names foreach (name => println(s"Hello, $name, I hope you enjoy the show."))
```

The => means it's a lambda.  The items to the left of it ('name' above) are the parameters, and the expression to the right is the result.

You might have connected this with some of the examples in [Looping](Looping.md), note that the above foreach and the below for-comprehension are the same thing:

```scala
for (name <- names)
  println(s"Hello, $name, I hope you enjoy the show.")
```

In fact the for-comprehension compiles into the foreach call with the lambda, but not all for-comprehensions compile that way.

The compiler does a good job at inferring the type of the lambda but sometimes it needs a hint.  For instance:

```scala
val plus = (x, y) => x + y
```

This won't compile, because the compiler can't tell whether x and y should be Ints, or some other type, i.e., there is no context.  You can provide a context easily by adding a type:

```scala
val plus: (Int, Int) => Int = (x, y) => x + y
```

Now try not to get dizzy, the change we made above was to add (Int, Int) => Int, which means 'a function that takes two Ints and returns an Int'.

If it helps you to understand the code, you can break the line at the = sign:

```scala
val plus: (Int, Int) => Int =
  (x, y) => x + y
```

Higher-Order Functions
======================

This fancy phrase just means functions that we can pass around as values.  Java doesn't have those, you can't pass Math.max around as a value, you can only call it.

We've already met the most common use of higher-order functions (can I call them HOFs from now on?  Thanks!), as parameters.  They can also be return types, i.e., a method or function can return a function.  This isn't as common, but it's worth knowing about:

```scala
def curriedPlus(x: Int): Int => Int =
  (y: Int) => x + y
```

Let's pick the signature (the first line) apart.. curriedPlus is a method that takes an Int (x) as a parameter, and returns a function.  That function itself takes an Int and returns an Int.  Let's use curriedPlus:

```scala
val plus5 = curriedPlus(5)
println(plus5(10)) // prints 15
println(plus5(15)) // prints 20
val plus7 = curriedPlus(7)
println(plus5(3) + plus7(6)) // what does this print?
```

Implicit Lambdas (Underscores)
==============================

If most of your lambdas look like x => x + 5, (x, y) => x * y, etc., i.e., you only use the parameter names once each, then you might get some truck out of the implicit lambda syntax:

```scala
println(List(10, 12, 13) filter (_ % 2 != 0)) // leaves us with 13, the only odd number
println(List(3, 6, 9) filter (_ / 3)) // leaves us with 1, 2, 3
println(List(1, 2, 4, 8, 16).foldLeft(0)(_ + _)) gives us 0 + 1 + 2 + 4 + 8 + 16, i.e., 31.
```

The rule there is that every underscore matches a new parameter, so _ + _ + _ + _ means the same as (a, b, c, d) => a + b + c + d, rather than a + a + a + a

It's not something you'll need to use because you can always use a lambda instead, but you might meet it or eventually decide to use it.

Exercises
=========

1. Write a method that takes an Int => String and calls it with the number 10, returning the result.

2. Write a method that takes an Int, we'll call it x, and returns "There are x bottles on the wall", where x should be the value of x, not the letter x.

3. Call the method in 1), passing it the method in 2), and print the result.

What Next
=========

[Collections](Collections.md)
