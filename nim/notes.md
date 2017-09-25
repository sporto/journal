# Notes about Nim

Couples of weeks ago I decided to start learning Nim. I got myself a copy of Nim in Action and started doing exercises in exercism.io.

## What is great about Nim

- Nim is quite easy to pick up, it has a very straighforward syntax
- Significant whitespace means less noise
- Enums that can resemble algebraic data types (ADTs)

## Things I'm not convinced about

- Not very convinced about the idea of style insensitve syntax, makes searching code harder
- Implicit `result` variable. Not sure why is this useful or desired. Seems to make the code more magical.
- Unqualified imports by default. Is hard to tell where stuff is coming from.

## What I don't like so far

- There is an `option` type in the standard libray. How come there is no `result` or `either` type?

- Building ADT types are more complex than necessary. And ADT is made like:

```
type
  MaybeKind = enum
    MaybeJust, MaybeNothing
  Maybe*[T] = object
    case kind: MaybeKind
    of MaybeJust:
      value: T
    of MaybeNothing:
      discard
```

When all we want is:

```
type Maybe*[T] = Nothing | Just T
```

- The way enum are defined we need to pass the types all the time.

- "Template" procs in sequtils are weird. E.g. `foldl`. This is trying to make the proc more terse. But at the end it less flexible. Why is this not just a proc that take a another proc? e.g. foldl(numbers, proc)

- No easy way to do partial application

- The language is unsafe

e.g. sequence access is unsafe seq[32]. It would be nice if this returned an option.

e.g. fields in objects can be nil

```
type
  Thing = object
    items: seq[int]

let thing = Thing()
thing.items 
```