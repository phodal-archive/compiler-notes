# Scala


## DSL in Scala

from: [https://stackoverflow.com/questions/49216312/what-is-dsl-in-scala](https://stackoverflow.com/questions/49216312/what-is-dsl-in-scala)

### infix method

```scala
someObject.someMethod(someArgument)

// can be written as

someObject someMethod someArgument
```

### trailing block argument

```scala
def someMethod(x: Int)(y: String) = ???

// can be invoked as
someMethod(42)("foo")

// but also as
someMethod(42) { "foo" }
```

###  last parameter is a function

```
def someOtherMethod[A, B](x: A)(f: A => B): B = ???

someOtherMethod(42) { a =>
  // ...a very long body
}
```

### custom methods to types

```
implicit class TimesOps(x: Int) {
  def times(y: Int): Int = x * y
}

// then use as

2 times 4 // 8
```
