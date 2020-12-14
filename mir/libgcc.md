# LibGCC

https://gcc.gnu.org/onlinedocs/gcc-9.1.0/jit/internals/index.html#overview-of-code-structure

### API calls

```bash
 /* Indentation indicates inheritance: */
  class context;
  class memento;
    class string;
    class location;
    class type;
      class function_type;
      class compound_type;
        class struct_;
	class union_;
      class vector_type;
    class field;
    class fields;
    class function;
    class block;
    class rvalue;
      class lvalue;
        class local;
	class global;
        class param;
      class base_call;
      class function_pointer;
    class statement;
    class case_;
```

### parse_file

```bash
  /* Indentation indicates inheritance: */
  class context;
  class wrapper;
    class type;
      class compound_type;
    class field;
    class function;
    class block;
    class rvalue;
      class lvalue;
        class param;
    class source_file;
    class source_line;
    class location;
    class case_;
```