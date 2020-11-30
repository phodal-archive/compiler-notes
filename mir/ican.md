# ICAN XBNF

Source: [http://www.cs.tau.ac.il/~msagiv/courses/acd/](http://www.cs.tau.ac.il/~msagiv/courses/acd/)


MIRInst -> | ReceiveInst | AssignInst | GotoInst | IfInst | CallInst | ReturnInst | SequenceInst | Lable: MIRInst 
ReceiveInst -> receive VarName(ParamType)
AssignInst