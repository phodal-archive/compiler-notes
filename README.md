# compiler-notes


## Refs

### Comby

[Comby](https://github.com/comby-tools/comby) is a tool for structural code search and replace that supports ~every language. 

Template

```
if :[expr] != nil {
  for :[x] := range :[expr] {
    :[body]
  }
}
```

match code

```
for :[x] := range :[expr] {
  :[body]
}
```

Comby DSL in code

```ocaml
open MParser

module Syntax = struct
  include Generic.Syntax

  let escapable_string_literals =
    [ {|"|}
    ; {|'|}
    ]

  let escape_char =
    '\\'

  let raw_string_literals =
    []

  let comment_parser s =
    (Parsers.Comments.c_multiline
     <|> Parsers.Comments.c_newline) s
end

include Matcher.Make(Syntax)
```

### Instaparse

 - [https://github.com/Engelberg/instaparse](https://github.com/Engelberg/instaparse)

 Instaparse aims to be the simplest way to build parsers in Clojure.

 - Turns standard EBNF or ABNF notation for context-free grammars into an executable parser that takes a string as an input and produces a parse tree for that string.
 - No Grammar Left Behind: Works for any context-free grammar, including left-recursive, right-recursive, and ambiguous grammars.
 - Extends the power of context-free grammars with PEG-like syntax for lookahead and negative lookahead.
 - Supports both of Clojure's most popular tree formats (hiccup and enlive) as output targets.
 - Detailed reporting of parse errors.
 - Optionally produces lazy sequence of all parses (especially useful for diagnosing and debugging ambiguous grammars).
 - "Total parsing" mode where leftover string is embedded in the parse tree.
 - Optional combinator library for building grammars programmatically.
 - Performant.

| Category | Notations | Example |
|----------|-----------|---------|
| Rule | : := ::= = | S = A |
| End of rule | ; . (optional) | S = A; |
| Alternation | | | A | B |
| Concatenation | whitespace or , | A B |
| Grouping | () | (A | B) C |
| Optional | ? [] | A? [A] |
| One or more | + | A+ |
| Zero or more | * {} | A* {A} |
| String terminal | "" '' | 'a' "a" |
| Regex terminal | #"" #'' | #'a' #"a" |
| Epsilon | Epsilon epsilon EPSILON eps ε "" '' | S = 'a' S | Epsilon |
| Comment | (* *) | (* This is a comment *) |


Examples:

```coljure
;; Clojure
(:require [instaparse.core :as insta :refer [defparser]])
;; ClojureScript
(:require [instaparse.core :as insta :refer-macros [defparser]])

=> (time (def p (insta/parser "S = A B; A = 'a'+; B = 'b'+")))
"Elapsed time: 4.368179 msecs"
#'user/p
=> (time (defparser p "S = A B; A = 'a'+; B = 'b'+")) ; the meat of the work happens at macro-time
"Elapsed time: 0.091689 msecs"
#'user/p
=> (defparser p "https://gist.github.com/Engelberg/5283346/raw/77e0b1d0cd7388a7ddf43e307804861f49082eb6/SingleA") ; works even in cljs!
#'user/p
=> (defparser p [:S (c/plus (c/string "a"))]) ; still works, but won't do any extra magic behind the scenes
#'user/p
=> (defparser p "S = 1*'a'" :input-format :abnf :output-format :enlive) ; takes additional keyword arguments
#'user/p
```

Docs:

 - https://github.com/ericnormand/squarepeg.  A peg parser in Clojure inspired by OMeta 
 - [Parsley](https://github.com/cgrand/parsley).  a DSL for creating total and truly incremental parsers in Clojure 

