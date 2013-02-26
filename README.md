scala-training
==============

Scala Training Course for Java Programmers

Why Scala
=========

More and more clients are asking for Scala programmers, because it is an interesting language that hits the sweet spot between object-oriented and functional programming, it's incredibly compatible with Java, and unlike some of its competitors is still statically typed like Java - in fact more than Java is.

What does it look like?
=======================

Those classes in your code that have lots of getters (and possibly setters), some fields backing them, maybe a constructor that copies its parameters to fields,an equals/hashCode implementation, a toString, here's what it looks like in Scala:

    case class Employee(id: Int, name: String, role: Role)

The callbacks that infest most client-side Java development and some server-side, with an anonymous class implementing some interface with a single method:

    button addActionListener (e => println("An event happened"))

Those monster generics declarations just to introduce an explaining variable:

    val foo = someCall(args) // you can specify the type if you like

No semi-colons.  Unlike JavaScript where you don't need semi-colons but should add them, in Scala there's no real benefit to adding them.

How do I set it up?
===================

Go to http://typesafe.com/stack/download , tick to accept the terms and submit, then choose a way of installing depending on your OS.  Note that the Windows one should work without being an administrator, just choose somewhere you can write to.

While you're there you can download the Scala IDE, which is a prepackaged version of Eclipse with the Scala plugins installed.  As always with Eclipse it doesn't need installing, only unpacking.

The IntelliJ IDEA plugin wasn't working for me at the time of writing, probably because I'm on an IDEA alpha version.  There's a plugin for Netbeans too, but I haven't tried it, and there are modes for vim and emacs.

Hello World
===========

Open the Scala IDE.  Create a new Scala Project, and start typing into a new Scala file:

    object Main extends App {
      println("hello world")
    }

Note there's no static, everything static needs to go in an 'object', which behaves like a class that only contains static methods except it's actually an instance that gets created automatically.

App is a trait (like an interface) that exists just to make sure the object can be executed as if it were a Java main class, but we don't need to implement a main method, we can just place the statements in the object's body.
