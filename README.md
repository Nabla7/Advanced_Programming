# Advanced Programming

## Chapter 1:

### Introduction

- **Flexibility towards multiple Programming Paradigms**
  - Procedural, Object-Oriented, Generic paradigms
- **Developer has Control**
  - Optimization of memory management and CPU usage
- **Language Feature**: Compiled

### C++: Compiled vs Interpreted Languages

- **Compiled Languages**
  - Source code converted to executable machine code before runtime.
  
- **Interpreted Languages**
  - Source code converted to executable machine code at runtime.

### C++ Compiler Phases

1. **Preprocessor**
   - Source code preprocessed using macros (start with #).

2. **Compiler**
   - Preprocessed source code converted to executable machine code.
   - One object file per source file.

3. **Linker**
   - Object files linked to create one executable file.

4. **Loader**
   - Executable code loaded into memory for execution.

### C++ Timings

- Source File -> Preprocessing -> Compile Time -> Linking Time -> Executable File -> Loading Time -> Runtime

### Binding

- **Definition**: Associating properties with names.
  
- **Binding Times**:
  ![]
  - Type of x: Compile time
  - Reference to do_something*: Linking time
  - Memory location for x: Loading time
  - Memory location & value of y: Runtime
  - Value of x: Runtime

### Static vs Dynamic Binding

- **Static Binding**: Occurs before runtime, remains unchanged.
  
- **Dynamic Binding**: Occurs during execution, can change.

### Static vs Dynamic Semantics

- **Static Property**: Pertains to source code, determined from source code.
  
- **Dynamic Property**: Occurs during execution, inferred from execution.

### Static vs Dynamic Types

- **Static Type**: Type of expression determined without considering execution semantics.
  
- **Dynamic Type**: Type of the most derived object to which expression refers.
  - Every variable has both a static type and a dynamic type.
  
- **Examples**:
  - Variable base: Static=Base, Dynamic=Base
  - Variable derived: Static=Derived, Dynamic=Derived
  - Variable b: Static=Base, Dynamic=Base or Derived
  - Variable b: Static=Base, Dynamic changes from Base to Derived

### Declarations & Definitions

- **Declaration**: Introduces identifier, binds its static type. Needed for compiler.
  
- **Definition**: Instantiates/implements identifier. Needed for linker.
  
- **Note**: A definition can also be a declaration.

- **Identifier Rules**:
  - Can be declared multiple times.
  - Must be defined once.

### One Definition Rule

- No multiple definitions for variables, functions, class types, enumeration types, or templates.
  
- Every program must contain one definition of every non-inline function or variable used.
  
- One class definition required if any translation unit where the class is used requires it.

### Takeaways:
- No definition leads to ambiguity.
- Multiple definitions create confusion on which to choose.
