Methods
=======

A few examples of various kinds of methods:

```scala
object MethodExamples {
  def noArgsNoResult {
    println("useful code here")
  }

  def argsNoResult(name: String) {
    println(s"Hello, $name") //look, string interpolation.
  }

  def argsAndResult(name: String, age: Int): String = name + ": " + age // no braces

  def withGenerics[A](list: List[A]): A = list.head // fails on an empty list

  def twoArgLists(x: Int)(y: Int): Int = x + y // used as twoArgLists(3)(4)
}
```

If it starts with def, it's a method.  If you use it as a value, it's a function:

```scala
def twiceTheValue(x: Int) = x * 2

val sixEightTen = List(3, 4, 5) map twiceTheValue // twiceTheValue is a value here, hence it's a function.
```

You can leave off the return type as the compiler can figure it out in most cases, but it's worth adding to make understanding your code easier.

Note that the return keyword isn't needed in most methods, but if you want to break out of a loop early you'll need it (or a different way of [Looping](Looping.md)):

```scala
def firstNumberWhoseSquareIsAbove500: Int = {
  var x = 0
  while (true) {
    if (x * x > 10)
      return x
    x += 1 //no x++ here, we use ++ to join two collections instead.
  }
}
```

Exercises
========

1. Define a method that takes three Ints as parameters, and returns the smallest.

2. Define a method that takes no parameters and prints out the value of System.currentTimeMillis.

3. Define a method that takes in a value of any type and returns that value.  I should be able to use it as: val three: Int = identity(3) and val hello = identity("hello")

What Next
========
[Looping](Looping.md)
