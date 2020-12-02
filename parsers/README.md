[Modern Parser Generator](https://matklad.github.io/2018/06/06/modern-parser-generator.html)

## Related

[Fall](https://github.com/matklad/fall)

Rust:

 - [https://github.com/pest-parser/pest](https://github.com/pest-parser/pest)
 - [https://github.com/Geal/nom](https://github.com/Geal/nom)
 - [https://github.com/lalrpop/lalrpop](https://github.com/lalrpop/lalrpop)

IDEA:

 - [https://github.com/Eliah-Lakhin/papa-carlo](https://github.com/Eliah-Lakhin/papa-carlo)

Others

 - [https://github.com/tree-sitter/tree-sitter](https://github.com/tree-sitter/tree-sitter)


## Antlr vs BNF

# Grammar Syntax

|                               | BNF                           | ISO EBNF                      | ABNF                          | ANTLR                         |
|:-----------------------------:|:-----------------------------:|:-----------------------------:|:-----------------------------:|:-----------------------------:|
| rule definition               | `<name> ::= ...`              | `name = ... ;`                | `name = ...`                  | `name : ... ;`                |
| terminal items                | `...`                         | `'...'` or `"..."`            | integer or `"..."`            | `'...'`                       |
| non-terminal items            | `<...>`                       | `...`                         | `...` or `<...>`              | `...`                         |
| concatenation                 | (space)                       | `,`                           | (space)                       | (space)                       |
| choice                        | `|`                           | `|`                           | `/`                           | `|`                           |
| optional                      | requires choice syntax[^1]    | `[...]`                       | `*1...` or `[...]`            | `...?`                        |
| 0 or more repititions         | requires choice syntax[^2]    | `{...}`                       | `*...`                        | `...*`                        |
| 1 or more repititions         | requires choice syntax[^3]    | `{...}-`                      | `1*...`                       | `...+`                        |
| n repititions                 |                               | `n*...`                       | `n*n...`                      |                               |
| n to m repititions            |                               |                               | `n*m...`                      |                               |
| grouping                      |                               | `(...)`                       | `(...)`                       | `(...)`                       |
| comment                       |                               | `(*...*)`                     | `;...`                        | `// ...` or `/* ... */`       |


[^1]: `optionalb ::= a b c d | a c d`

[^2]: `list ::= | listitem list`

[^3]: `list ::= listitem | listitem list`