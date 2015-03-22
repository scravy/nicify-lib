nicify
======

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



```
    >>> runhaskell main.hs | nicify
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


