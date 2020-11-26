# Core CLR

[JIT Compiler Structure](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/ryujit-overview.md)

```code
   r1 = (-b + Math.Sqrt(b*b - 4*a*c))/(2*a);
```

output

```bash
STMT  (IL 0x000...0x026)
   ▌  ASG       double
   ├──▌  IND       double
   │  └──▌  LCL_VAR   byref  V03 arg3
   └──▌  DIV       double
      ├──▌  ADD       double
      │  ├──▌  NEG       double
      │  │  └──▌  LCL_VAR   double V01 arg1
      │  └──▌  INTRINSIC double sqrt
      │     └──▌  SUB       double
      │        ├──▌  MUL       double
      │        │  ├──▌  LCL_VAR   double V01 arg1
      │        │  └──▌  LCL_VAR   double V01 arg1
      │        └──▌  MUL       double
      │           ├──▌  MUL       double
      │           │  ├──▌  LCL_VAR   double V00 arg0
      │           │  └──▌  CNS_DBL   double 4.0000000000000000
      │           └──▌  LCL_VAR   double V02 arg2
      └──▌  MUL       double
         ├──▌  LCL_VAR   double V00 arg0
         └──▌  CNS_DBL   double 2.0000000000000000
```
