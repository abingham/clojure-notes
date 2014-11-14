# ns #

Makes a namespace active. Generally at top of file.

```clojure
(ns path.of.namespace
(:use [some.package :as other]
      [another.package :only [name1 name2]])
```

# use and require #

# Functions #

```
(defn func-name
  "docstring"
  [arg1 arg2 arg3]
  (implementation))
```

# Multimethods #

Multimethods select between various implementations based on a
dispatch function.

## defmulti ##

This defines the API of the multimethod, as well as the dispatch method.

```
(defmulti apply-event
  "Apply an event to a state, returning a new state."
  (fn [event state] (:type event)))
```

The dispatch function defines the signature for the function, and what
it does is return some value that implementations of the function will
match.

## defmethod ##

```
(defmethod apply-event
  :rename
  [event state]
  (let [name (:name event)]
    (assoc state :name name)))

(defmethod apply-event
  :resize
  [event state]
  (let [new-size (:size event)]
  (assoc state :size new-size)))

(apply-event {:type :rename :name "Alice"} {:name "Bob :size 4})
=> {:name "Alice" :size 4}
```

# Interfaces and data structures #

## defprotocol ##

Define a protocol.

```
(defprotocol Flubbable
  (flub [this x])
  (unflub [this]))
```

## deftype ##

Define a type. Typically used for programming or system constructs.

```
(deftype File [name size])
(.name (->File "answer" 42))
=> answer
```

Types can implement protocols either in their definition or
extrinsically.

```
(deftype File [name size]
 Flubbable
 (flub [this x] (...)))

(extend-type File
 Borkable
 (bork [this] (...)))
```

## defrecord ##

Define a record. Much like `deftype`, but records are also
`IPersistentMap`s. They are typically used for "domain" data rather
than programming constructs.

```
(defrecord Widget [foo bar baz])
(:foo (->Widget 1 2 3))
=> 1
(.baz (->Widget 1 2 3))
=> 3
```

Records can implement protocols in exactly the same way as types.

# Concurrency #

dosync, alter, commute, etc.

## refs ##

## atoms ##

## agents ##

# Java interop #
