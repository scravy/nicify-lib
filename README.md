nicify-lib
==========

[![Build Status](https://travis-ci.org/scravy/nicify.svg?branch=master)](https://travis-ci.org/scravy/nicify)

`nicify` is a tool for pretty printing the default formatting of `Show` instances.
It is especially useful when dumping data during debugging.

Example
-------

Given `main.hs`:

```haskell
data X = A [X] | B String | C (X, X)
  deriving (Show)

main = print $
  A [B "one", B "two", A [ C (B "three", B "three prime"), B "woop woop" ]]
```

you would typically get:

```
>>> runhaskell main.hs 
A [B "one",B "two",A [C (B "three",B "three prime"),B "woop woop"]]
```

not so with nicify:

```haskell
import Text.Nicify

data Z = A [Z] | B String | C (Z, Z)
  deriving (Show)

main = putStrLn . nicify . show
  $ A [B "one", B "two", A [ C (B "three", B "three prime"), B "woop woop" ]]
```

results in:

```
>>> runhaskell main.hs -package nicify-lib
A [
    B "one",
    B "two",
    A [
        C (B "three",
        B "three prime"),
        B "woop woop"
    ]
]
```

`nicify` is also available as command line tool, see
[`github.com/scravy/nicify`](https://github.com/scravy/nicify)
