Variables
=========

Val
===

    val a = 5 // defaults to Int
    val b: Int = 5 // explicitly adding the type, rare but sometimes useful.
    val c: Double = 5 // overriding the default
    val d = 5.0 // defaults to Double

    println(a + b) // 10
    a = a + b // error, a is a val, you can't change it.
    a += b // error, same reason

Var
===

    var a = 5
    var b: String = "hello"
    a += 10
    b += " world"

Generally try to use vals instead of vars where possible, unless you have a choice between a val referring to a mutable object or a var referring to an immutable object.

Lazy Val
========

    lazy val x = 5 / 0 // if we never read x, no exception happens.
    lazy val y: String = "foo"

This appears occasionally as a way of avoiding an expensive computation, but generally you should be trying to use val.

Why is there no Lazy Var?
=========================

Because it doesn't make sense to have one.  You can write a container that behaves like that if you like, but you'll probably find it confusing.
