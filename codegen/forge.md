# Forge

```
Types:

ftpe(args, ret, freq)
  define a new function type (args) => ret

tpePar(name)
  define new type parameter
tpe(name, tpePars, stage)
  define new type
tpeClass(name, tpePars)
 define new type class
tpeClassInst(name, tpePars, tpeClass)
 define new type class instance

Data structures:

data(tpe, (fieldName,fieldTpe)*)
 associate tpe with the given struct
impl(op, allocates(tpe))
  implementation pattern to allocate a struct
impl(op, getter(tpe,field))
 implementation pattern to read a field
impl(op, setter(tpe,field))
 implementation pattern to write a field

Annotations:

effect ::= simple | mutable | write | error
 declare an op has the corresponding effect semantic
freq ::= hot | cold | normal
 code motion hints
stage ::= now | future
  declare whether a generated type should be T or Rep[T]
aliasHint ::= nohint | contains(arg) | copies(arg)
 declares relationships between operations and inputs

Methods:

arg(name,tpe,default)
 define a new op argument
static | infix | direct | compiler | fimplicit (grp, name, tpePars, signature, effect, aliasHint)
  defines a new op with the specified syntax style and parameters
(args :: retTpe)
  defines a new method signature
impl(op, codegen | single | composite | map | filter | groupby | reduce | zip | foreach)
  defines the implementation for an op based on a predefined pattern

Miscellaneous:

grp(name)
  declares a group of ops that do not belong to a type
extern(name)
  declares an op group implemented in external code
lift(grp)(tpe)
  declares a conversion from the given tpe to a Rep[.]
lookupOp | lookupGrp | lookupTpe (name)
 returns a previously declared DSL construct
withTpe(tpe)
  construct a new syntactic scope

Parallel Collections:
parallelize(tpe) as ParallelCollection | ParallelCollectionBuffer (ops)
 declares that the provided type implements a ParallelCollection interface with the given ops
```
