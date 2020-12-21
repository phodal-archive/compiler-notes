# Related

## Semantic

Languages: Haskell

[GitHub Semantic](https://github.com/github/semantic) is a Haskell library and command line tool for parsing, analyzing, and comparing source code.


## tree-sitter

[Tree-sitter](https://github.com/tree-sitter/tree-sitter) is a parser generator tool and an incremental parsing library. It can build a concrete syntax tree for a source file and efficiently update the syntax tree as the source file is edited. Tree-sitter aims to be:

 - General enough to parse any programming language
 - Fast enough to parse on every keystroke in a text editor
 - Robust enough to provide useful results even in the presence of syntax errors
 - Dependency-free so that the runtime library (which is written in pure C) can be embedded in any application


```haskell
{
  // ...

  rules: {
    source_file: $ => repeat($._definition),

    _definition: $ => choice(
      $.function_definition
      // TODO: other kinds of definitions
    ),

    function_definition: $ => seq(
      'func',
      $.identifier,
      $.parameter_list,
      $._type,
      $.block
    ),

    parameter_list: $ => seq(
      '(',
       // TODO: parameters
      ')'
    ),

    _type: $ => choice(
      'bool'
      // TODO: other kinds of types
    ),

    block: $ => seq(
      '{',
      repeat($._statement),
      '}'
    ),

    _statement: $ => choice(
      $.return_statement
      // TODO: other kinds of statements
    ),

    return_statement: $ => seq(
      'return',
      $._expression,
      ';'
    ),

    _expression: $ => choice(
      $.identifier,
      $.number
      // TODO: other kinds of expressions
    ),

    identifier: $ => /[a-z]+/,

    number: $ => /\d+/
  }
}
```

## Redex

[Redex](https://docs.racket-lang.org/redex/) consists of a domain-specific language for specifying reduction semantics, plus a suite of tools for working with the semantics.

```haskell

(define-language L
  (e (e e)
     (λ (x t) e)
     x
     (amb e ...)
     number
     (+ e ...)
     (if0 e e e)
     (fix e))
  (t (→ t t) num)
  (x variable-not-otherwise-mentioned))
```



