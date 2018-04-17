---
layout: post
title:  "Creating an \"iterable\" in Scala"
date:   2018-04-17
categories: scala
---
How do we create data structure that can be used as a generator in the *for* expression?

It turns out that one just need to define *map* and *flatMap*. Why? See
[expansion rules *for*](https://www.scala-lang.org/files/archive/spec/2.11/06-expressions.html#for-comprehensions-and-for-loops)
but in essence it turns out that

    for (p <- e) yield e′

is translated to

    e .map { case p => e′ }.

and

    for (p <- e; p′ <- e′;…) yield e″

is translated to

    e.flatMap { case p => for (p′ <- e′;…) yield e″ }


#### Example:

Generator below can't be used in the *for*

```
trait GeneratorWeak[+T] {
  def generate: T
}

val integers = new GeneratorWeak[Int] {
  val rand = new java.util.Random

  def generate:Int = rand.nextInt()
}

integers.generate

// At this point we cannot create booleans generator with for (compiler complains about missing map)
val booleans = for { i : Int <- integers } yield i > 0

// or pairs generator like
def pairs[T, U](u: GeneratorWeak[U], t: GeneratorWeak[T]): GeneratorWeak[(T, U)] = for {
    x <- u
    y <- t
  } yield (x, y)

pairs(integers, booleans).generate

```

as compiler complains about map and flatMap being missing so let's add those:
```
trait Generator[+T] {
  upper =>

  def generate: T

  def map[S](f: T => S): Generator[S] = new Generator[S] {
    def generate: S = f(upper.generate)
  }

  def flatMap[S](f: T => Generator[S]): Generator[S] = new Generator[S] {
    def generate: S = f(upper.generate).generate
  }
}

val integers2 = new Generator[Int] {
  val rand = new java.util.Random()

  override def generate: Int = rand.nextInt()
}

// with map defined in Generator we can already do booleans generator with for
val booleans2: Generator[Boolean] = for {i <- integers2} yield i > 0

booleans2.generate
booleans2.generate
booleans2.generate

// and with flatMap we can generate generators with multiple enumerator expressions

def pairs2[T, S] (t: Generator[T], s: Generator[S]): Generator[(T, S)] = for{
  x <- t
  y <- s
} yield (x, y)

val pairs_generator = pairs2(integers2, booleans2)
pairs_generator.generate
```

and voila!
