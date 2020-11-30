# ICAN XBNF

Source: [http://www.cs.tau.ac.il/~msagiv/courses/acd/](http://www.cs.tau.ac.il/~msagiv/courses/acd/)

## Version 1

The main program

```
Program -> [label:] ProgUnit*
ProgUnit -> [label:] begin MIRInsts end
MIRInsts -> {[label:] MIRInst [|| Comment]}*
Label -> Identifier
MIRInst -> ReceiveInst | AssignInst | GotoInst | IfInst
MIRInst -> CallInst | ReturnInst | SequenceInst
```

The receive instruction

```
ReceiveInst -> receive varname (ParamType)
ParamType -> val | res | valres | ref
```

Assignments

```
AssignInst -> VarName <- Expression
AssignInst -> VarName <- (VarName) Operand
AssignInst -> [*]VarName[.EltName] <- Operand
Expression -> Operand BinOper Operand
Expression -> UnaryOper Operand | Operand
Operand -> VarName | Const
BinOper -> + | - | * | / | mod | min | max | RelOper
BinOper -> shl | shr | shra | and | or | xor | . | *.
RelOper -> = | != | < | <= | > | >=
UnaryOper -> - | ! | addr | (TypeName) | *
```

Control flow instructions

```
GotoInst -> goto Label
IfInst -> if RelExpr {goto Label | trap Const}
RelExpr -> Operand RelOp Operand | [!] Operand
```

Call/Return instructions

```
CallInst -> [call | VarName <- ] ProcName, Arglist
ArgList -> ([{Operand,TypeName}<>;])
ReturnInst -> return [Operand]
```

Constants

```
Const -> Integer | FloatNumber | Boolean | nil
Integer  ->  0 | [-] NZDecDigit DecDigit*
Integer  ->  0x HexDigit*
NZDecDigit  ->  1 | 2 | … | 9
DecDigit  ->  0 | NZDecDigit
HexDigit  ->  DecDigit| a | … | f | A | … | F
FloatNumber  ->  [-] DecDigit+ .DecDigit+ [E [-] DecDigit+][D]
Boolean  ->  true | false
```

Identifiers

```
Label -> Identifier
VarName -> Identifier
EltName -> Identifier
Identifier -> Letter {Letter | DecDigit | _}*
```


## Version 2
