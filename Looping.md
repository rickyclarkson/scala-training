Looping
=======

Scala has the familiar do and while loops from Java:

```scala
do
  println("bob")
while (true)

while (true)
  println("bob")
```

It does not have an equivalent to the pre-Java 5 for loop, but its for-comprehensions can do what we usually use a for loop for:

```scala
for (i <- 1 to 10)
  println(i * i)
```

The for-comprehension is roughly equivalent to .NET's LINQ, it's really very flexible:

```scala
for (i <- 1 to 10 if !(i % 3 == 0))
  println(i) // printing only the numbers not divisible by 3

for (i <- 1 to 10; j <- i to 10)
  println(i + ", " + j)

for { i <- 1 to 10
      j <- i to 10 }
  println(i + ", " + j // same as above but with different formatting.

val squares = for (i <- 1 to 10) yield i * i // stores a collection of 1, 4, 9, 16, 25.. 100 in the variable squares.
```

Another option is a fold (related to reduce from Map/Reduce), if we have a method 'plus' that adds two numbers then folding plus over a List is like writing all the elements of the List out with a + between them:

```scala
def plus(x: Int, y: Int) = x + y
val sum = List(3, 4, 5).foldLeft(0)(plus) // the same as writing 0 + 3 + 4 + 5
```

Left above means that it's like ((0 + 3) + 4) + 5 and not 0 + (3 + (4 + 5)), if that's confusing just use foldLeft always.

Exercises
=========

1. Write a program that reads at least one random number from math.random and keeps retrieving them until it hits one that's less than 0.2, printing the last one out.

2. Write a program that, for the numbers from 1 to 100, prints Fizz if the number is a multiple of 3, Buzz if it's a multiple of 5, FizzBuzz if it's a multiple of both, or the number itself otherwise.  Here's 1 to 17 as an example:

   1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz, 16, 17

   It doesn't matter if you print them out next to each other or on separate lines.

What Next
=========

Let's zip along to [pattern-matching](Patterns.md).
