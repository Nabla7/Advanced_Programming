## **Advanced Programming in C++** 

### Slides provided by Brent Van Bladel

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

# Chapter 2 : **Functions**

- **Purpose**: 
  - Break programs into smaller, simpler pieces.
  - Enhance structure, readability, and comprehension.
  - Abstraction and self-documenting.
  - Reusability & reduced redundancy.

### **Function Terminology**
- **Type**: Refers to the return value type.
  ```cpp
  int functionName(); // "int" is the type.
  ```
  
- **Signature**: Function name + parameter types.
  ```cpp
  void display(int, double); // "display(int, double)" is the signature.
  ```

- **Prototype**: Type + signature (function declaration).
  ```cpp
  int sum(int, int); // This is a prototype.
  ```

### **Declaration vs Definition**
- **Declaration**: Prototype + optional function specifiers such as `inline`, `constexpr`, `noexcept`, `nodiscard`, and more. 

  ```cpp
  inline int square(int x); // Declaration with "inline" specifier.
  ```

- **Definition**: Declaration + function body.

  ```cpp
  int square(int x) { 
      return x*x; 
  } // This is a definition.
  ```

### **Inline Functions**
- A suggestion to the compiler to expand the function in line when called.
- Advantages:
  - Speeds up program by avoiding function call overhead.
  - Allows function definitions in header files.
- Disadvantages:
  - Increases executable size.
  - Inlining is resolved at compile time, increasing compilation time.
  ```cpp
  inline int add(int a, int b) {
      return a + b;
  }
  ```

### **Constexpr Functions**
- Evaluated at compile-time.
- Advantages:
  - Faster execution by avoiding function call and calculation overhead.
  - Reduces executable size.
- Disadvantages:
  - Increases compile time.
  - Limited usability.
  ```cpp
  constexpr int factorial(int n) {
      return (n <= 1) ? 1 : n * factorial(n - 1);
  }
  ```

### **Noexcept Functions**
- Indicates the function doesn't throw exceptions.
- Optimizations based on this.
  ```cpp
  int divide(int a, int b) noexcept {
      return (b != 0) ? a / b : 0;
  }
  ```

### **Nodiscard Functions**
- Ensures return value should be used.
  ```cpp
  [[nodiscard]] int compute();
  ```

### **Function Overloading & Resolution**
- Functions with the same name but different parameters.
- Compiler tries to find the best match.
  ```cpp
  void display(int a);
  void display(double b);
  ```

### **Namespaces**
- **Purpose**: Avoid name conflicts & logically group entities.
  ```cpp
  namespace Math {
      int add(int, int);
  }
  ```

- **Accessing Namespaces**:
  - **Explicit Qualification**: `namespace-name::member-name`
    ```cpp
    Math::add(1, 2);
    ```
  - **Using-Directives**: Introduce a namespace into the scope.
    ```cpp
    using namespace Math;
    ```
  - **Using-Declarations**: Introduce a synonym in the scope.
    ```cpp
    using Math::add;
    ```

- **Unnamed Namespaces**: Auto included in current scope.
  ```cpp
  namespace {
      void internalFunction();
  }
  ```

- **Namespace Management**:
  - **Nesting**: Hierarchical topology.
  - **Composition**: Merge disjunct namespaces.
  - **Selection**: Select entities from various namespaces.
  - **Extension**: Add to existing namespace.
  - **Alias**: Alternative names for a namespace.
    ```cpp
    namespace MathOps = Math;
    ```

# Chapter 3 : Memory Management

### **Memory Concepts**
* **Variable**: An abstraction of memory space.
  * **Attributes**:
    * **Name**: How to reference in program.
    * **Address**: Memory location.
    * **Type**: Data interpretation.
    * **Storage Duration**: When memory is available.
    * **Lifetime**: When memory can be referenced.
    ```cpp
    int x;  // Name: x, Type: int, Storage Duration: automatic
    ```

### **Memory Areas: Stack vs Heap**
* **Stack**:
  * For local variables, function arguments, control information.
  * Faster, but limited in size.
  ```cpp
  int local_variable = 42;  // Stored on the stack
  ```
* **Heap**:
  * For dynamic memory allocation.
  * Flexible in size but slower.
  ```cpp
  int* heap_var = new int(42);  // 42 is stored on the heap
  ```

### **Variable Storage and Duration**
* Four Storage Durations:
  * **Automatic**: Lives within its scope.
  * **Static**: Lives for program's duration.
  * **Thread**: Lives for the thread's duration.
  * **Dynamic**: Lives between allocation & deallocation.
  ```cpp
  static int persist_var = 10;  // Static storage duration
  ```

### **Lifetime of Variables**
* Duration from memory allocation to memory release.

### **Memory in C++: Examples**
* A focus on bits and bytes allocation in various scenarios.
  ```cpp
  bool flag;  // Allocates 8 bits in memory
  ```

### **Vector Capacity & Memory**
* Understanding how `std::vector` allocates and grows memory.
  ```cpp
  std::vector<int> vec = {1, 2, 3};  // Memory allocated on stack & heap
  ```

### **Strings & Memory**
* `std::string` implementation.
  * How strings are stored on stack and heap.
  * **Short String Optimization (SSO)**: Storing short strings on stack.
  ```cpp
  std::string short_str = "Hi";  // Likely uses SSO
  ```

### **Copying Strings**
* **Deep Copy**: Entire data is duplicated.
* **Shallow Copy**: Only references are copied.
  ```cpp
  std::string str1 = "Hello";
  std::string str2 = str1;  // Deep copy
  ```

### **Optimizing String Operations**
* **`std::string_view`**: A non-owning reference to a string.
  * Avoids costly deep copies.
  ```cpp
  std::string_view sv = "example";  // No dynamic allocation
  ```

### **Passing Variables**
* **By Reference**: Efficient, no additional memory.
* **By Pointer**: Uses memory for pointer storage.
  ```cpp
  void func_by_ref(int& x);
  void func_by_ptr(int* x);
  ```

### **Special Memory Concepts**
* **nullptr**: Represents a null pointer.
* **`std::optional`**: Extends type domain by adding a "null" value without dynamic memory allocation.

# Chapter 4: Classes & Memory

### **Classes**
* A user-defined type abstracting a concept.
  * Groups data forming a broader concept.
  * Links functionality to data.
  
  ```cpp
  class Dog {
      string name;
      int age;
      
      public:
          void bark() { cout << "Woof!"; }
  };
  ```

### **Class vs. Object**
* Classes serve as blueprints, objects are instances of those blueprints.

  ```cpp
  Dog myDog;  // myDog is an object of the Dog class
  ```

### **Memory Layout of a Class**
* Visual representation showing memory allocations in classes.

  ```cpp
  class Coordinate {
      int x, y;  // memory layout sequentially in most cases
  };
  ```

### **Constructors**
* Explicit method to initialize an object.
  ```cpp
  class Dog {
      string name;
      public:
          Dog(string n) : name(n) {}
  };
  Dog rex("Rex");
  ```

### **Default Constructor**
* Initializes an object without specific data.
  ```cpp
  class Dog {
      public:
          Dog() {}
  };
  ```

### **Implicit Default Constructor**
* Automatically provided if no user-defined constructors exist.
  ```cpp
  class Dog {};  // Compiler creates default constructor implicitly
  ```

### **Default Keyword**
* Request compiler to generate a default constructor.
  ```cpp
  class Dog {
      public:
          Dog() = default;
  };
  ```

### **In-Class Initializers**
* Data members initialized within class definition.
  ```cpp
  class Dog {
      int age = 5;
  };
  ```

### **Member Initializer Lists**
* More efficient than assigning values in the constructor body.
  ```cpp
  class Rectangle {
      int width, height;
      public:
          Rectangle(int w, int h) : width(w), height(h) {}
  };
  ```

### **Copy Constructor**
* Initializes one object using another object of the same class.
  ```cpp
  class Dog {
      public:
          Dog(const Dog &d) { /* ... */ }
  };
  ```

### **Copy Constructor vs Assignment Operator**
* Understanding the difference in operation.
  ```cpp
  Dog d1 = d2;     // Copy constructor
  d1 = d2;         // Assignment operator
  ```

### **Bracket Initialization vs Parentheses**
* Always opt for braced initialization.
  ```cpp
  Dog d1{"Rex"};   // Braced initialization
  Dog d2("Rex");   // Parentheses, but be careful with ambiguities
  ```

### **Destructors**
* Method to destroy an object.
  ```cpp
  class Dog {
      public:
          ~Dog() { /* Cleanup code here */ }
  };
  ```
