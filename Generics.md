Generics
========

Scala has similar syntax to Java where generics are concerned, except that it uses [], e.g., List[A], and instead of extends and super it uses <: and >:

```scala
class Foo[A] {
  import scala.collection.mutable.ListBuffer
  private val secretListBuffer = new ListBuffer[A]
  def receive(a: A) = secretListBuffer += a
  def last: A = secretListBuffer.last
}

def sort[A <: Comparable[A]](a: A, b: A, c: A) = {
  val min = math.min(math.min(a, b), c)
  val max = math.max(math.max(a, b), c)
  val other = a + b + c - min - max
  (min, other, max) // a tuple
}
```
