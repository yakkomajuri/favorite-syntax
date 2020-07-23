# Compilation of Favorite Syntax from r/ProgrammingLanguages Members

## Python

#### Generator Expressions (u/ibrahimqasim & u/usernamecreationhell)

```python
evens = [i for i in range(100) if i % 2 == 0]
squares = [i**2 for i in evens]
pairs = [(x,y) for x in range(100) for y in range(100)]
squarepairs = [(i, i**2) for i in range(100) if i % 2 == 0]
```

#### Variable Unpacking & Multiple Assignment  (u/ibrahimqasim)

```python
x, y, z = (4, 5, 6)
x, *xs = [1, 2, 3, 4]
x, y = 4, 5
```

#### With blocks (u/Beefster09)

```python
with open(filename, 'w') as file:
    file.write("Hello world\n")
```

## Haskell 

#### Do Notation (u/superstar64)

```haskell
import Control.Monad.Trans.State

-- chaining optionals
optionChain :: Maybe (Int, a)
optionChain = do
 left <- Just 1
 right <- Nothing
 return (left,right)

-- combining side effects
sideEffects :: IO ()
sideEffects = do
 print "Hello"
 print "World"

-- argument sharing
shareArguments :: Int -> Bool
shareArguments = do
 x <- (+1)
 y <- (+2)
 return (x == y)
 
 -- nondeterministic functions
nondeterministic :: [Bool]
nondeterministic = do
 first <- [True,False]
 second <- [True,False]
 return (first && second)

-- OPP-like state
implicitState :: State Int Bool
implicitState = do
 this <- get
 put (this + 1)
 return (this == 0)

-- generic code for all monads
combine :: Monad context => context left -> context right -> context (left,right)
combine runLeft runRight = do
 left <- runLeft
 right <- runRight
 return (left,right)
```


#### List Comprehensions (u/batllista101)

```haskell
nats = [1..]
evens = [i | i <- nats, even i]  
squares = [i^2 | i <- evens]
pairs = [(x,y) | x <- [0..99], y <- [0..99]]
```

### Variable Unpacking & Multiple Assignment (u/batllista101)

```haskell
(x, y, z) = (4, 5, 6)
(x, xs) = [1, 2, 3, 4]
(x, y) = (4, 5)
```

## OCaml

#### Anonymous Functions (u/Yul3n)

```ocaml
let rec fib = function | 0 -> 0 | 1 -> 1 | n -> fib (n - 1) + fib (n - 2)
```

## C

#### Bracket-less Control Structures (u/Yul3n)

```c
for (int i = 0; i < 5; ++i) printf("%d\n", i);
```

## JavaScript

#### Array Destructuring (u/That-Thou-Art)

```js
const arr = [1, 2, 3]

// This:
let [a, b, c] = arr

// Is the same as this:
let a = arr[0], b = arr[1], c = arr[2]
```

## Go

#### Variable/Constant Declaration and Import Blocks (u/almbfsek)

```go
var (
    x int
    y int
)

// same as this
var x int
var y int
```

#### Receiver Functions (u/almbfsek)

```go
type Y struct {
    someVar int
}

func (y *Y) doStuffWithY(x int) {
    y.someVar = ...
}

// the above is exactly the same as
func doStuffWithY(y *Y, x int) {
    y.someVar = ...
}
```

## Scala

#### Case Classes (u/Adriandmen)

For example, something simple like defining a Tree class:
```scala
sealed trait Tree[A]

case class Branch[A](l: Tree[A], r: Tree[A], v: A) extends Tree[A]
case class Leaf[A](v: A)                           extends Tree[A]
```

Then summing up the tree can be done like this:
```scala
def sum(tree: Tree[Int]): Int = tree match {
  case Branch(l, r, v) => sum(l) + sum(r) + v
  case Leaf(v) => v
}
```

## Nim 

#### Flexible Call Syntax
```nim
# All of these mean the same thing
foo(bar)
bar.foo()
bar.foo
foo bar
foo:
  bar
```

And with multiple arguments:
```nim
foo(bar, baz)
bar.foo(baz)
bar.foo baz
foo bar, baz
foo(bar):
  baz
```

#### Style Insensitivity

All of these are the same: `fooBarBaz`, `foo_bar_baz`, `foobarbaz`, `fOObA_Rb_aZ`. However, they're distinct from `FooBarBaz`.

This means that you can use the same style across your codebase even if your modules use a different style.

#### Pragmas

Pragmas remove the need for keywords like inline and you can easily define your own. They can be used in many different places.
```nim
proc double[T](x: T): T {.inline, noSideEffects.} =
  2 * x
```

#### Result Variable

Every procedure automatically defines a variable called result, which is initialized to the default value and automatically returned at the end unless you explicitly return something else. This allows for succint code like this:

```nim
proc sum(arr: openArray[int]): int =
  for num in arr:
    result += num
```
