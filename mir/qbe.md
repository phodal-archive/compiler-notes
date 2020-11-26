# QBE

[https://c9x.me/compile/](https://c9x.me/compile/)

## Sample

### hello, world

```javascript
# Define the string constant.
data $str = { b "hello world", b 0 }

function w $main() {
@start
        # Call the puts function with $str as argument.
        %r =w call $puts(l $str)
        ret 0
}
```

### loop

```javascript
function $loop() {
@start
@loop
        %x =w phi @start 100, @loop %x1
        %x1 =w sub %x, 1
        jnz %x1, @loop, @end
@end
        ret
}
```


more

```javascript
function w $add(w %a, w %b) {              # Define a function add
@start
	%c =w add %a, %b                   # Adds the 2 arguments
	ret %c                             # Return the result
}
export function w $main() {                # Main function
@start
	%r =w call $add(w 1, w 1)          # Call add(1, 1)
	call $printf(l $fmt, w %r, ...)    # Show the result
	ret 0
}
data $fmt = { b "One and one make %d!\n", b 0 }
```

## Instructions

*   [Arithmetic and Bits](https://c9x.me/compile/doc/il.html#Arithmetic-and-Bits):
    *   `add`
    *   `and`
    *   `div`
    *   `mul`
    *   `or`
    *   `rem`
    *   `sar`
    *   `shl`
    *   `shr`
    *   `sub`
    *   `udiv`
    *   `urem`
    *   `xor`
*   [Memory](https://c9x.me/compile/doc/il.html#Memory):
    *   `alloc16`
    *   `alloc4`
    *   `alloc8`
    *   `loadd`
    *   `loadl`
    *   `loads`
    *   `loadsb`
    *   `loadsh`
    *   `loadsw`
    *   `loadub`
    *   `loaduh`
    *   `loaduw`
    *   `loadw`
    *   `storeb`
    *   `stored`
    *   `storeh`
    *   `storel`
    *   `stores`
    *   `storew`
*   [Comparisons](https://c9x.me/compile/doc/il.html#Comparisons):
    *   `ceqd`
    *   `ceql`
    *   `ceqs`
    *   `ceqw`
    *   `cged`
    *   `cges`
    *   `cgtd`
    *   `cgts`
    *   `cled`
    *   `cles`
    *   `cltd`
    *   `clts`
    *   `cned`
    *   `cnel`
    *   `cnes`
    *   `cnew`
    *   `cod`
    *   `cos`
    *   `csgel`
    *   `csgew`
    *   `csgtl`
    *   `csgtw`
    *   `cslel`
    *   `cslew`
    *   `csltl`
    *   `csltw`
    *   `cugel`
    *   `cugew`
    *   `cugtl`
    *   `cugtw`
    *   `culel`
    *   `culew`
    *   `cultl`
    *   `cultw`
    *   `cuod`
    *   `cuos`
*   [Conversions](https://c9x.me/compile/doc/il.html#Conversions):
    *   `dtosi`
    *   `exts`
    *   `extsb`
    *   `extsh`
    *   `extsw`
    *   `extub`
    *   `extuh`
    *   `extuw`
    *   `sltof`
    *   `stosi`
    *   `swtof`
    *   `truncd`
*   [Cast and Copy](https://c9x.me/compile/doc/il.html#Cast-and-Copy) :
    *   `cast`
    *   `copy`
*   [Call](https://c9x.me/compile/doc/il.html#Call):
    *   `call`
*   [Variadic](https://c9x.me/compile/doc/il.html#Variadic):
    *   `vastart`
    *   `vaarg`
*   [Phi](https://c9x.me/compile/doc/il.html#Phi):
    *   `phi`
*   [Jumps](https://c9x.me/compile/doc/il.html#Jumps):
    *   `jmp`
    *   `jnz`
    *   `ret`

