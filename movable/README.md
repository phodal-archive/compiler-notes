 
- DSL
- template inheritance


## Template

 - Info
 	- name
 	- extensions<>
 - Syntax
    - user_defined_delimiters
 	- raw_string_literals
 	- escapable_string_literals
 	- comments

```ocaml
module Javascript = struct
  module Info = struct
    let name = "JavaScript"
    let extensions = [".js"]
  end

  module Syntax = struct
    include Dyck.Syntax

    let raw_string_literals =
      [ ({|`|}, {|`|})
      ]

    let escapable_string_literals =
      Some
        { delimiters = [{|"|}; {|'|}; {|/|}]
        ; escape_character = '\\'
        }

    let comments =
      [ Multiline ("/*", "*/")
      ; Until_newline "//"
      ]
  end
end
```
