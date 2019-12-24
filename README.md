# Programming Paradigms - Worksheet Three

Even more predictable than last time...

We will be continuing with the exercises from the <https://www.scala-exercises.org> site.

1. Got to the site.
2. Login with your nice new shiny `GitHub` account.
3. Follow the [`Scala Tutorial`][tut] path (click on the `Start` button) - just in case you had forgotten.

For this week you should complete the remaining exercises.

+ SYNTACTIC CONVENIENCES

def greet(name: String): String =
  s"Hello, $name!"

greet("Scala") shouldBe "Hello, Scala!"
greet("Functional Programming") shouldBe 
"Hello, Functional Programming!"

def greet(name: String): String =
  s"Hello, ${name.toUpperCase}!"

greet("Scala") shouldBe 
"Hello, SCALA!"

TUPLES

def pair(i: Int, s: String): (Int, String) = (i, s)

pair(42, "foo") shouldBe ((42, "foo"))
pair(0, "bar") shouldBe 
(0, "bar")

Manipulating Tuples
You can retrieve the elements of a tuple by using a tuple pattern:

val is: (Int, String) = (42, "foo")

is match {
  case (i, s) =>
    i shouldBe 42
    s shouldBe 
"foo"

}
Or, simply:

val is: (Int, String) = (42, "foo")

val (i, s) = is
i shouldBe 42
s shouldBe 
"foo"
Alternatively, you can retrieve the 1st element with the _1 member, the 2nd element with the _2 member, etc:

val is: (Int, String) = (42, "foo")
is._1 shouldBe 42
is._2 shouldBe 
"foo"

Default Values

case class Range(start: Int, end: Int, step: Int = 1)

val xs = Range(start = 1, end = 10)

xs.step shouldBe 
1

Repeated Parameters

def average(x: Int, xs: Int*): Double =
  (x :: xs.to[List]).sum.toDouble / (xs.size + 1)

average(1) shouldBe 1.0
average(1, 2) shouldBe 1.5
average(1, 2, 3) shouldBe 
2

TYPE ALIASES

type Result = Either[String, (Int, Int)]
def divide(dividend: Int, divisor: Int): Result =
  if (divisor == 0) Left("Division by zero")
  else Right((dividend / divisor, dividend % divisor))
divide(6, 4) shouldBe Right((1, 2))
divide(2, 0) shouldBe Left("Division by zero")
divide(8, 4) shouldBe 
Right((2,0))




[tut]: https://www.scala-exercises.org/scala_tutorial
