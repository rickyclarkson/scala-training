Pattern-matching
================

Switch on steroids.  First, let's cover what Java's switch can be used for:

```scala
digit match {
  0 => println("null")
  1 => println("ein")
  2 => println("zwei")
  3 => println("drei")
  _ => println("I'm sorry, I can't go past 3 in German")
}
```

It can also return a value, i.e., it's an expression:

```scala
val german = digit match {
  0 => "null"
  1 => "ein"
  2 => "zwei"
  3 => "drei"
  _ => "I'm sorry, I can't go past 3 in German"
}
```

It's a bit unsatisfactory that the default case above is still a String, we might want to handle it differently.  'throw' works:

```scala
  _ => throw new IllegalStateException("I'm sorry, I can't go past 3 in German")
```

but even so, we might want to reflect that in the return type.  We have a type, Option (coming in Java 8 as Optional) that can represent Some(element) or None:

```scala
val german: Option[String] = digit match { // we can leave off the : Option[String] if we want.
  0 => Some("null")
  1 => Some("ein")
  2 => Some("zwei")
  3 => Some("drei")
  _ => None
}
```

Given german, an Option[String], we might want to print out the value unless it's None:

```scala
println(german match {
  case None => "I'm sorry"
  case Some(t) => t
})
```

We can even match over Arrays:

```scala
val actual = Array(3, 10, 12)
actual match {
  case Array(x, y, z) => println(x + y * z)
}

val actual = Array(3, 10, 12)
val Array(x, y, z) = actual //alternative syntax, pattern-matching in a declaration, creating 3 variables.
println(x + y * z)
```

We can write recursive operations on Lists (Lists are single-linked lists, i.e., a non-empty list has a value and a tail, where the tail is a List):

```scala
def sum(list: List[Int]): Int = list match {
  case Nil => 0 // if it's an empty list, give 0
  case value :: tail => value + sum(tail) // if it's a value and a tail, add the value to the result of summing the tail
}
```

You can use it to replace instanceof and casts, though this has most of the same problems as instanceof and casts:

```scala
trait Vehicle // like an empty Java interface.
class Car extends Vehicle
class Bike extends Vehicle

val someVehicle: Vehicle = new Car

someVehicle match {
  case c: Car => println("It's a car")
  case b: Bike => println("It's a bike")
}
```

If you add another type, e.g., a Boat, the compiler won't help you to get this right and you'll get an exception at runtime.  It will, however, if the trait is sealed (can only be extended in the same source file):

```scala
sealed trait Animal
class Cow extends Animal
class Sheep extends Animal
class Dog extends Animal

val someAnimal: Animal = new Dog
someAnimal match { // this gives us a compiler warning, because the match is incomplete (misses out Dog)
  case c: Cow => println("It's a cow")
  case s: Sheep => println("It's a sheep")
}
```

You can combine a few cases if their code would be the same:

```scala
println(number match {
  case 5 | 9 | 14 => "One of my lucky numbers"
  case 13 | 7 | 666 => "One of my unlucky numbers"
})
```

Pattern-matching has some more to it, but we probably won't need any more than this.
