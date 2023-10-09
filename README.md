## **Advanced Programming in C++** 

# Chapter 1 : Basics

### **Introduction**
* Flexibility towards multiple **Programming Paradigms**
  * Procedural, Object-Oriented, Generic paradigms
* **Developer's Control**:
  * Allows optimization of memory management and CPU usage
* **Language Type**: Compiled
  * This means C++ code is converted into machine code before being executed, leading to faster executions.

### **C++: Compiled vs Interpreted Languages**

* **Compiled Languages**:
  ```cpp
  // Example of C++ code
  #include<iostream>
  int main() {
    std::cout << "Hello, World!";
    return 0;
  }
  ```
  Code is converted to machine code before runtime.

* **Interpreted Languages**:
  ```python
  # Example in Python
  print("Hello, World!")
  ```
  Code is interpreted and executed on-the-fly.

### **C++ Compiler Phases**

1. **Preprocessor**:
   ```cpp
   // Example
   #include<iostream>
   #define PI 3.14159
   ```
   Source code is preprocessed using macros that start with `#`.

2. **Compiler**:
   Produces object files. E.g., `main.o` from `main.cpp`

3. **Linker**:
   Combines multiple object files and libraries into one executable.

4. **Loader**:
   Loads the executable into memory for execution.

### **C++ Timings**

* A depiction of how a C++ source file goes through various phases from writing to execution.

### **Binding**

* **Definition**: Associating properties with names.

* **Binding Times**:
  ```cpp
  int x; // Type binding happens at compile time
  void do_something(); // Reference binding is at linking time
  ```
  - Type of `x`: Compile time
  - Reference to `do_something()`: Linking time
  - Memory location for `x`: Loading time

### **Static vs Dynamic Binding**

* **Static Binding**:
  ```cpp
  void function() {
    std::cout << "Static bound function.";
  }
  ```
  The function is bound at compile-time.

* **Dynamic Binding**:
  ```cpp
  class Base {
  public:
    virtual void show() {
      std::cout << "In Base";
    }
  };

  class Derived : public Base {
  public:
    void show() {
      std::cout << "In Derived";
    }
  };
  ```
  Function binding occurs at runtime based on the object type.

### **Static vs Dynamic Semantics**

* **Static Property**: Determined without execution.
  
* **Dynamic Property**: Based on runtime behaviors.

### **Static vs Dynamic Types**

* Variables have both static and dynamic types. The static type is known at compile time, while the dynamic type is determined at runtime.

### **Declarations & Definitions**

* **Declaration**:
  ```cpp
  extern int x; // declaring without defining
  ```
  
* **Definition**:
  ```cpp
  int x = 5; // defining
  ```

* **Identifier Rules**: 
  An identifier can be declared multiple times but defined only once.

### **One Definition Rule**

* Important to avoid linker errors.
  
* If you have a function or a variable defined in multiple places, it creates confusion for the linker.

### **Key Takeaways**:
* No definition creates ambiguity.
* Multiple definitions create confusion on which to select.
