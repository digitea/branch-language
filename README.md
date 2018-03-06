# *Branch* Programming Language (DRAFT)

The world's first *branch based* programming language.

File extension: `.brnc`

## Why?

Branches are often complex in programming, and this if often made more difficult than it has to be due to the way that these are handled in some languages.
By imposing functional restrictions to the language, the complexity can be greatly reduced.
*Branch* does so by redifining what functional programming is.

## How?

Here are some defining traits:

+ Every "method" is a new *functional branch*.
+ *Functional branches* must have a return value.
+ Immutability is heavily promoted.
+ *Functional branches* should be highly parallelizable.
+ There are no `null` values.
+ There is no `void`.

Data types:

| Symbol          | Type                       | Description                            |
|:----------------|:---------------------------|:---------------------------------------|
| `bool`          | Primitive                  | boolean `true`/`false`                 |
| `float`         | Alias of `float(2)`        |                                        |
| `float(n)`      | Primitive                  | n-point floating point number          |
| `change`        | Primitive extending `data` | mutation of a `state` type             |
| `collection<p>` | Collection                 | collection of primitives with type `p` |
| `data`          | Primitive                  | immutable object                       |
| `int`           | Alias of `int(32)`         |                                        |
| `int(n)`        | Primitive                  | n-bit integer                          |
| `state`         | Primitive extending `data` | non-immutable object                   |
| `string`        | Primitive                  | text string                            |

## Syntax

```
data Argument {
    string name
    int value
}

data arg := Argument {
    name := "Name"
    value := 0
}

state State {
    int count := 0
}

// <- is state mutation
change commit := state.count <- state.count + 1
// commit.field
// commit.old
// commit.new (expected)
state.count <- 0

branch main (collection<string> args) int {
    int x := 1
    := x - 1
}

branch value (int in) : int {
    in + 1
}

branch test (data params) : bool {
    := param.results // collection<data>
        -> sum(result -> { result.count }) // int
        -> >= 5 // bool
}

branch result (bool increment, collection<int> values) : int {
    := increment ? {
        := values
            -> map(value -> value + 1)
            -> sum
    } : {
        := values
            -> sum
    }
}

branch b (data obj) int := obj.num
```
