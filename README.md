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

+ OBJECT ORIENTED PROGRAMMING

DYNAMIC BINDING


Empty contains 1 shouldBe 
false

new NonEmpty(7, Empty, Empty) contains 7 shouldBe 
true

abstract class Reducer(init: Int) {
  def combine(x: Int, y: Int): Int
  def reduce(xs: List[Int]): Int =
    xs match {
      case Nil => init
      case y :: ys => combine(y, reduce(ys))
    }
}

object Product extends Reducer(1) {
  def combine(x: Int, y: Int): Int = x * y
}

object Sum extends Reducer(0) {
  def combine(x: Int, y: Int): Int = x + y
}

val nums = List(1, 2, 3, 4)

Product.reduce(nums) shouldBe 
24

Sum.reduce(nums) shouldBe 
10

+ IMPERATIVE PROGRAMMING

val x = new BankAccount
val y = new BankAccount
x deposit 30
x withdraw 20 shouldBe 
10

def factorial(n: Int): Int = {
  var result = 
1

  var i = 
1

  while (i <= n) {
    result = result * i
    i = i + 
1

  }
  result
}

factorial(2) shouldBe 2
factorial(3) shouldBe 6
factorial(4) shouldBe 24
factorial(5) shouldBe 120

+ CLASSES VS CASE CLASSES

val aliceAccount = new BankAccount
val c3 = Note("C", "Quarter", 3)

c3.name shouldBe 
"C"

EQUALITY
val aliceAccount = new BankAccount
val bobAccount = new BankAccount

aliceAccount == bobAccount shouldBe 
false


val c3 = Note("C", "Quarter", 3)
val cThree = Note("C", "Quarter", 3)

c3 == cThree shouldBe 
true

val c3 = Note("C", "Quarter", 3)
c3.toString shouldBe 
"Note(C,Quarter,3)"

val d = Note("D", "Quarter", 3)
c3.equals(d) shouldBe 
false

val c4 = c3.copy(octave = 4)
c4.toString shouldBe 
"Note(C,Quarter,4)"

+ POLYMORPHIC TYPES
def size[A](xs: List[A]): Int =
  xs match {
    case Nil => 
0

    case y :: ys => 
1
 + size(ys)
  }
size(Nil) shouldBe 0
size(List(1, 2)) shouldBe 2
size(List("a", "b", "c")) shouldBe 3

+ LAZY EVALUATION

var rec = 0
def streamRange(lo: Int, hi: Int): Stream[Int] = {
  rec = rec + 1
  if (lo >= hi) Stream.empty
  else Stream.cons(lo, streamRange(lo + 1, hi))
}
streamRange(1, 10).take(3).toList
rec shouldBe 
3

val builder = new StringBuilder

val x = { builder += 'x'; 1 }
lazy val y = { builder += 'y'; 2 }
def z = { builder += 'z'; 3 }

z + y + x + z + y + x

builder.result() shouldBe 
"xzyz"

+ TYPE CLASSES

val compareRationals: (Rational, Rational) => Int = 
(x,y) => ( if (x.numer*y.denom>y.numer*x.denom) 1 else if (x.numer*y.denom==y.numer*x.denom) 0 else -1)


implicit val rationalOrder: Ordering[Rational] =
  new Ordering[Rational] {
    def compare(x: Rational, y: Rational): Int = compareRationals(x, y)
  }

val half = new Rational(1, 2)
val third = new Rational(1, 3)
val fourth = new Rational(1, 4)
val rationals = List(third, half, fourth)
insertionSort(rationals) shouldBe List(fourth, third, half)


[tut]: https://www.scala-exercises.org/scala_tutorial
