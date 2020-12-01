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

once match code replace to

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

first origin version:


```
./comby -stdin 'printf(":[1] :[2]")' 'printf("comby, :[1]")' << EOF 2> /dev/null
int main(void) {
  printf("hello world");
}
EOF
```

Outputs:

```c
int main(void) {
  printf("comby, hello");
}
```
- Adding a `-json` flag will output JSON content of the rewrite:

```json
[
  {
    "range": {
      "start": { "offset": 19, "line": -1, "column": -1 },
      "end": { "offset": 41, "line": -1, "column": -1 }
    },
    "replacement_content": "printf(\"comby, hello\")",
    "environment": [
      [
        "1",
        {
          "value": "hello",
          "range": {
            "start": { "offset": 15, "line": -1, "column": -1 },
            "end": { "offset": 20, "line": -1, "column": -1 }
          }
        }
      ]
    ]
  }
]
```

- Adding a `-match-only` flag will output JSON content of all matches:

```json
[
  {
    "range": {
      "start": { "offset": 19, "line": 1, "column": 20 },
      "end": { "offset": 40, "line": 1, "column": 41 }
    },
    "environment": [
      [
        "1",
        {
          "value": "hello",
          "range": {
            "start": { "offset": 27, "line": 1, "column": 28 },
            "end": { "offset": 32, "line": 1, "column": 33 }
          }
        }
      ],
      [
        "2",
        {
          "value": "world",
          "range": {
            "start": { "offset": 33, "line": 1, "column": 34 },
            "end": { "offset": 38, "line": 1, "column": 39 }
          }
        }
      ]
    ],
    "matched": "printf(\"hello world\")"
  }
]
```



### Cubix

[Cubix](https://github.com/cubix-framework/cubix) is a framework for language-parametric program transformation, i.e.: defining a single source-to-source program transformation tool that can be run on multiple languages. In Cubix, you can write transformations with a type signature like "This transformation works for any language that has assignments, loops, and a name-binding analysis," and instantly get separate tools for C, Java, etc. 

Code examples: [https://github.com/cubix-framework/rwus](https://github.com/cubix-framework/rwus)  The RWUS (Real World, Unchanged Semantics) benchmark suite for testing multi-language semantics-preserving source-to-source transformations 


Cubix is the world's first framework that can build language-parametric
source-to-source transformations. As the first of its kind, it often
gets mistaken for a solution to more familiar problems. In particular,
it is not:

* A tool for translating one language into another. Cubix allows you
  to create a single tool that can transform C programs into better C
  programs and Java programs into better Java programs. It is not
  designed for building tools that can transform C programs into Java programs. Indeed, much of
  its power comes from its ability to preserve all the information of
  the original program.
* A collection of ready-to-use refactoring tools. Thus far, all
  transformations built on Cubix are tech demos. While a couple are
  theoretically useful, they have not undergone the amount of UX
  engineering needed to actually be time-savers.
 * A framework for writing multi-language program analyses. Cubix transformations may consume results
   provided by other analyses, which may be written in either a
   single-language or multi-language fashion.
 * A framework for analysis/transformation of polyglot programs, i.e.:
   programs (or single source files) written in multiple
   languages. 
   
However, Cubix's generic-programming capabilities make it a powerful
tool for building all kinds of programming tools, even for only one
language. We are particularly excited about the potential of extending Cubix to
transform polyglot programs.

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

