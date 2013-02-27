Collections
===========

Scala's collections are primarily split into mutable and immutable ones.  The general aim is to default to immutable collections.  Let's explain how that can work without crippling the programmer.

You can't change an immutable collection any more than you can change a String.  However, you can make a new version, and Scala's immutable collections have clever ways of sharing most of the structure of a collection when you create a new one.  Let's take the most obvious example of that, an immutable singly-linked list:

```scala
println(List(3, 4, 5))
println(3 :: 4 :: 5 :: Nil)
```

Those two lines print the same thing, because the first is a shortcut for the second.  Let's deconstruct it:

* Nil is the empty list
* 5 :: Nil is a list whose value is 5 and whose tail is Nil
* 4 :: 5 :: Nil is a list whose value is 4 and whose tail is 5 :: Nil
* 3 :: 4 :: 5 :: Nil is a list whose value is 3 and whose tail is 4 :: 5 :: Nil

Because of List's structure it's O(n) in many operations, and O(n^2) in sorts, so it's clearly not optimal.  It is simple though, which is strongly in its favour.

Vector is a good alterative to List, it's still immutable, but it has O(1) times for most operations and shares over 95% of the structure when you create a modified version, so it's not very wasteful.

```scala
println(Vector(3, 4) + 5) // Vector(3, 4, 5)
println(Vector(3) ++ Vector(6, 9)) // Vector(3, 6, 9)
println(Vector(36, 81, 4096) map math.sqrt) // Vector(6, 9, 64)
```

You can convert from one collection type to another by using the 'to' method:

```scala
println(List(3, 4).to[Vector]) // Vector(3, 4)
println(Vector(3, 5, 3).to[Set]) // Set(3, 5) or Set(5, 3)
```
