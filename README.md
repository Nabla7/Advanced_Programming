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

  # Chapter 5: Advanced Memory

  ### **Memory Exercises**

### What is the output of this code?

```cpp
int main()
{
    int n = 1;
    int&& ref = n;
    cout << n << endl;
    cout << ref << endl;
    return 0;
}
```

### Output:
Compilation error: 
```
cannot bind rvalue reference of type 'int&&' to lvalue of type 'int'
```

---

### Summary & Clarification:

The code attempts to bind an rvalue reference (`int&&`) to an lvalue (`n`). In C++, rvalue references are primarily used to represent temporary objects that can be safely moved from. However, `n` is not a temporary object, it's an lvalue. This causes the compilation error.

To fix this error, one should either:
1. Use an lvalue reference (`int&`).
2. Bind the rvalue reference to an actual rvalue or temporary object.

---

## What is the output of this code?

```cpp
int main()
{
    int n = 1;
    int&& ref = std::move(n);
    cout << n << endl;
    cout << ref << endl;
    return 0;
}
```

### Output:
Probably "`1 1`", but there's no guarantee `n` remains consistent after the move.

### Summary & Clarification:

The code attempts to bind an rvalue reference (`int&&`) to `n` using `std::move`, which casts its argument into an rvalue. This allows for the binding to be successful. However, after performing a move, the state of the moved-from object (in this case, `n`) is unspecified but valid. That means the value might still be `1`, but it's not guaranteed. This behavior is dependent on the specific type and its implementation. For fundamental types like `int`, the value usually remains unchanged after a move, but it's best not to rely on that.

---

## What is the output of this code?

```cpp
int main()
{
    int n = 1;
    double&& rref = n;
    cout << n << endl;
    cout << rref << endl;
    return 0;
}
```

### Output:
`1 1`

### Summary & Clarification:

The code binds an rvalue reference of type `double` (`double&&`) to the integer variable `n`. When `n` is assigned to `rref`, an implicit conversion takes place, creating a temporary `double` with value `1.0`. The rvalue reference `rref` binds to this temporary. The output reflects this conversion with both `n` and `rref` displaying the value "1".

---

### 1. Binding a Non-Const Reference to an Rvalue

```cpp
void print(int& x){
    cout << x << endl;
}
int main(){
    print(5);
    return 0;
}
```

**Output**: Compiler error: "cannot bind non-const lvalue reference of type 'int&' to an rvalue of type 'int'."

**Explanation**: This example tries to bind a non-const reference (`int& x`) to an rvalue (`5`). Non-const references require an lvalue, but here we have an rvalue (`5`). This results in a compiler error since you can't modify a literal directly.

---

### 2. Binding a Const Reference to an Rvalue

```cpp
void print(const int& x){
    cout << x << endl;
}
int main(){
    print(5);
    return 0;
}
```

**Output**: 5

**Explanation**: This example demonstrates binding a const reference to an rvalue. Const references can bind to rvalues without any issues. The `const int&` accepts the literal `5`, and the temporary lifetime of `5` is extended for the duration of the function call.

---

### 3. Attempting to Bind a Return Value to a Non-Const Reference

```cpp
class Foo{
    private:
        int x{0};
    public:
        int getX() { return x; };
        void print() { cout << x << endl; };
};

int main(){
    Foo foo;
    int& x_ref = foo.getX();
    x_ref = 10;
    foo.print();
    return 0;
}
```

**Output**: Compiler error: "cannot bind non-const lvalue reference of type 'int&' to an rvalue of type 'int'."

**Explanation**: In this example, the `getX` method returns an integer by value, producing an rvalue. The code attempts to bind this rvalue to a non-const reference (`int& x_ref`). This is not allowed and thus results in a compiler error. To modify the internal `x` of the `Foo` class using a reference, the method `getX` should return a reference.

---

### What is the output of this code?

```cpp
class Foo{
    private:
        int x{0};
    public:
        int& getX() { return x; };
        void print() { cout << x << endl; };
};

int main(){
    Foo foo;
    int& x_ref = foo.getX();
    x_ref = 10;
    foo.print();
    return 0;
}
```

**Output**: 10

**Explanation**: In this example, the `getX` method returns a reference to the integer `x` (an lvalue-reference). This means that when `int& x_ref = foo.getX();` is executed, `x_ref` refers to the same memory location as the `x` in the `Foo` object. Thus, modifying `x_ref` directly changes the value of `x`. The `foo.print()` function will then output the modified value of `x`, which is `10`.

---

### What is the output of this code?

```cpp
class Foo{
    private:
        int x{0};
    public:
        int& getX() { return x; };
        void print() { cout << x << endl; };
};

int main(){
    Foo foo;
    foo.getX() = 10;
    foo.print();
    return 0;
}
```

**Output**: 10

**Explanation**: Here, the `getX` method returns a reference to the integer `x` (an lvalue-reference). This means you can directly assign a value to what it returns. In the line `foo.getX() = 10;`, the value of `x` inside the `Foo` object is set to `10`. The `foo.print()` function then outputs this value, which is `10`.

**Note**: This behavior can be prevented by having the `getX` method return a `const int&` instead of `int&`, thereby ensuring that the returned reference cannot be used to modify the value of `x`.

---


### What is the output of this code?

```cpp
int& getNumber(){
    int x = 5;
    return x;
}

int main(){
    cout << getNumber() << endl;
    return 0;
}
```

**Output**: Undefined behaviour

**Explanation**: The function `getNumber` is returning a reference to a local variable `x`. Once the function exits, the local variable goes out of scope, resulting in the returned reference being a "dangling reference". This means it refers to a memory location that is no longer valid, leading to undefined behavior when trying to access it in the `main` function.

**Note**: A dangling reference is a reference that outlives the lifetime of the object it refers to. Always ensure that you don't return references to local variables to avoid such issues.

---

### What is the output of this code?

```cpp
int& getNumber(){
    static int x = 5;
    return x;
}

int main(){
    cout << getNumber() << endl;
    return 0;
}
```

**Output**: 5

**Explanation**: In this code, the function `getNumber` returns a reference to a static local variable `x`. Unlike normal local variables, static local variables retain their values between function calls and have a lifetime from the start of the program until the end of the program. Therefore, returning a reference to a static local variable is safe, and there's no danger of dangling references in this case.

**Note**: A static variable has a static storage duration, and a lifetime from the start of the program until the end of the program.

---

### What is the output of this code?

```cpp
int&& getNumber(){
    int x = 5;
    return std::move(x);
}

int main(){
    cout << getNumber() << endl;
    return 0;
}
```

**Output**: Undefined behaviour.

**Explanation**: The function `getNumber` returns an rvalue-reference (`int&&`) to a local variable `x`. Despite using `std::move` to turn `x` into an rvalue, the underlying issue remains: the local variable `x` will be destroyed when the function exits, leaving the reference dangling. Accessing this dangling reference, as done in the `main` function, leads to undefined behavior.

**Note**: An rvalue-reference is still a reference, and can become a dangling reference when it refers to an object whose lifetime has ended.

---

### What is the output of this code?

```cpp
int getNumber(){
    int x = 5;
    return std::move(x);
}

int main(){
    cout << getNumber() << endl;
    return 0;
}
```

**Output**: 5

**Explanation**: The function `getNumber` returns a prvalue (pure rvalue), which would normally be created by copying the local variable `x` to a temporary. Using `std::move` in this case turns `x` into an xvalue (expiring value). However, since `x` is of a simple built-in type (`int`), moving and copying are effectively the same, and the behavior is well-defined. The function returns the value of `x`, which is 5.

**Note**: Using `std::move` with simple built-in types offers no real benefit and can be confusing. It's primarily useful for complex objects that have a move constructor which can perform a shallow copy, transferring ownership of resources and avoiding deep copy operations.

---

### What is the output of this code?

```cpp
int* getNumber(){
    int* x_ptr = new int(5);
    return x_ptr;
}

int main(){
    cout << *getNumber() << endl;
    return 0;
}
```

**Output**: 5

**Explanation**: The function `getNumber` dynamically allocates an integer on the heap with a value of 5 and returns its pointer. The main function then dereferences this pointer to print the value, which is 5.

**Note**: This program contains a memory leak because the dynamically allocated memory in `getNumber` is not deallocated using `delete`. It's essential to free up the memory to avoid memory leaks, especially in larger applications.

---

### What is the output of this code?

```cpp
int* getNumber(){
    int* x_ptr = new int(5);
    delete x_ptr;
    return x_ptr;
}

int main(){
    cout << *getNumber() << endl;
    return 0;
}
```

**Output**: Undefined behaviour.

**Explanation**: The function `getNumber` dynamically allocates an integer on the heap with a value of 5. However, it then deletes this memory before returning the pointer. Dereferencing a deleted pointer in the main function leads to undefined behaviour. The program may crash, produce unexpected output, or seem to work correctly in some cases, but it's not reliable or safe.

**Note**: A pointer that points to a deleted memory location is known as a dangling pointer. It's crucial to ensure that you don't use pointers after their associated memory has been deallocated.

---

### What is the output of this code?

```cpp
struct Bar {
    int a{0};
    int b{0};
};

class Foo {
    private:
        const Bar& _bar;
    public:
        Foo(const Bar& b) : _bar(b) {};
        int sum() { return _bar.a + _bar.b; }
};

int main() {
    Foo foo{Bar{4,2}};
    cout << foo.sum() << endl;
    return 0;
}
```

**Output**: Undefined behaviour.

**Explanation**: The object `foo` in the `main` function is constructed with a temporary `Bar` object. Normally, temporaries are destroyed at the end of the full-expression in which they are created. However, the lifetime of the temporary `Bar` object is extended to match the lifetime of the reference parameter `b` in the `Foo` constructor. But once the constructor completes, the temporary `Bar` object goes out of scope, and `_bar` in `Foo` becomes a dangling reference. Subsequent usage of this reference, like in the `sum` method, leads to undefined behavior.

**Note**: A reference data member in a class or struct does use memory, typically the same amount as a pointer on the respective platform. It's essential to ensure the lifetime of the referenced object exceeds that of the object containing the reference.

---
