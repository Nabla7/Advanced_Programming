## **Advanced Programming in C++** 

### Slides provided by Brent Van Bladel

- [Chapter 1: Basics](#chapter-1-basics)
- [Chapter 2: Functions](#chapter-2-functions)
- [Chapter 3: Memory Management](#chapter-3-memory-management)
- [Chapter 4: Classes & Memory](#chapter-4-classes--memory)
- [Chapter 5: Advanced Memory](#chapter-5-advanced-memory)
- [Chapter 6: Class Design](#chapter-6-class-design)
- [Chapter 7: Class Derivation](#chapter-7-class-derivation)
- [Chapter 8: Design Patterns](#chapter-8-design-patterns)
- [Chapter 9: Multi-threading in C++](#chapter-9-multi-threading-in-c)
- [Chapter 10: Generic Programming](#chapter-10-generic-programming)

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
  
---

# **Chapter 5: Advanced Memory**

**Purpose**:
- Dive deep into the complex world of memory management in programming.
- Learn to allocate and deallocate resources efficiently.
- Understand how to prevent memory leaks, leading to optimal application performance.

---

## **Ownership**

**Purpose**:
- Master the concept of which code segment controls the duration of an object's existence.

**Detailed Explanation**:
- Ownership is a fundamental concept in C++ where every object or resource has a clear owner, usually a variable or a data structure. This owner is responsible for the resource's cleanup, ensuring no memory leaks.
  
    ```cpp
    Circle circleInstance;  // Here, the variable `circleInstance` owns the Circle object.
    ```

---

## **Smart Pointers**

**Purpose**:
- Understand the mechanisms that allow automated memory management.
- Learn how smart pointers are more efficient and safer than traditional raw pointers.

### *shared_ptr*:
- This is a type of smart pointer that permits multiple `shared_ptr` objects to share the ownership of a heap object. 
- It employs a reference counting mechanism, ensuring the heap object is deleted only when the last `shared_ptr` that points to it is destroyed or reset.

    ```cpp
    std::shared_ptr<int> ptr1 = std::make_shared<int>(5);
    ```

### *unique_ptr*:
- Another flavor of smart pointer that guarantees sole ownership of the allocated heap memory.
- While it doesn't allow duplication, ownership is transferable, ensuring resource safety.

    ```cpp
    std::unique_ptr<int> unique(new int(10));
    ```

---

## **Deleted Functions**

**Purpose**:
- Grasp the idea of deliberately rendering specific functions inaccessible to prevent unintended actions.

**Detailed Explanation**:
- By marking certain functions as deleted, C++ ensures they cannot be used in any context. This is particularly useful for preventing copying of unique pointers.

```cpp
unique_ptr(const unique_ptr&) = delete;  // This ensures a unique_ptr cannot be copied.
```

---

## **Copy Elision**

**Purpose**:
- Comprehend how C++ can optimize and bypass certain copy or move operations under specific circumstances.

**Detailed Explanation**:
- Copy elision is a compiler optimization where the compiler can omit unnecessary copy and move operations, leading to more efficient code generation.

---

## **Move Semantics**

**Purpose**:
- Understand the seamless transfer of resources from one object to another without the overhead of copying.

### *std::move*:
- A utility that enables resources of an object (like memory or file handles) to be moved rather than copied. This is especially useful for transferring ownership of dynamically allocated memory.

    ```cpp
    std::string str = "hello";
    std::string movedStr = std::move(str);  // 'str' content is moved to 'movedStr'.
    ```

### *Move Constructor & Move Assignment*:
- Special members that are invoked when resources are moved between objects, facilitating efficient resource management.

    ```cpp
    MyClass(MyClass&& other);  // Move constructor declaration.
    ```

---

## **C++ Value Categories**

**Purpose**:
- Get acquainted with the categorization of expressions based on their address properties.

### *lvalue*: 
- Expressions that have a stable address in memory. These are typically variables that persist beyond a single expression.

    ```cpp
    int x = 10;  // 'x' is an lvalue since it has an identifiable memory address.
    ```

### *prvalue*:
- Pure rvalue, typically temporary and doesn't associate with a persistent memory location.

    ```cpp
    int y = x + 5;  // 'x + 5' is a prvalue, representing a temporary result.
    ```

### *xvalue*:
- Denotes expiring values. They typically represent resources that can be moved from.

---

## **References**

**Purpose**:
- Dive deep into the aliases for variables and their utility.

### *lvalue reference*:
- Acts as an alias for an lvalue. It cannot bind to temporary objects (with a few exceptions).

    ```cpp
    int& ref = x;  // 'ref' is essentially another name for 'x'.
    ```

### *rvalue reference*:
- A new type of reference introduced to facilitate move semantics. It can bind to temporaries, aiding efficient resource utilization.

    ```cpp
    int&& rref = 10;  
    ```

---

## **Lifetime Extension**

**Purpose**:
- Understand how the life of temporary objects can be extended using references.

**Detailed Explanation**:
- Temporary objects usually have a short lifespan, restricted to a single expression. However, when a temporary object is bound to a const lvalue reference, its lifetime extends to the reference's lifetime.

```cpp
const int& tempRef = 5;  // The lifespan of '5', a temporary, is extended to match 'tempRef'.
```

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

# Chapter 6 : **Class Design**

### **Introduction**
* A class represents a user-defined data type, capturing both data (attributes) and behavior (methods).
* Provides a mechanism to encapsulate data and the functions that operate on the data.

### **Classes vs Structs**
* **Class**: Typically, members are private by default. Meant for complex data structures with both data members and methods.
* **Struct**: Members are public by default. Best used for passive data structures without behavior.
  
  ```cpp
  class MyClass {
      int a; // private by default
  public:
      void doSomething();
  };

  struct MyStruct {
      int a; // public by default
  };
  ```
* **Tip**: Use structs if all members are meant to be public.

### **Class Interface**
* Represents the set of public members (functions & attributes) that are exposed to users.
* **Abstract Data Type (ADT)**: A class interface, when designed well, should present an abstract view of the data, hiding the implementation details.

  ```cpp
  class Stack {
  public:
      void push(int);
      int pop();
  private:
      int arr[10];
      int top;
  };
  ```

### **Advantages of Class Interface**
* **Encapsulation**: Users don't need to know the inner workings.
* **Localization of Change**: Modifications inside the class won't affect external users as long as the interface remains consistent.

### **Class Interface - Header Files**
* Class interfaces are typically defined in header files (`ClassName.h`).
* Implementation of the class is defined in source files (`ClassName.cpp`).

### **#Include and Compilation**
* When using `#include`, the compiler essentially copies the content of the included file.
* **Dangers**:
  * One Definition Rule (ODR) violations.
  * Cyclic includes leading to infinite loop.

  ```cpp
  // File: main.cpp
  #include "Header1.h"
  #include "Header2.h"
  ```

### **Solutions to Compilation Dangers**
* **Include Guards**: Ensure the header file is only included once.
  * Utilize `#ifndef`, `#define`, and `#endif` preprocessor directives.
  ```cpp
  #ifndef REPORTER_H
  #define REPORTER_H
  // ... class/interface declaration
  #endif
  ```
* **Forward Declarations**: Declare a class/struct without defining it, which helps avoid cyclic dependencies.

### **Const Member Function**
* Indicates the member function won't modify the object's state.
  ```cpp
  int getValue() const { return value; }
  ```

### **Mutable Data Member**
* Allows a data member to be modified even inside a const member function.
  
  ```cpp
  class MyClass {
  mutable int cache;
  int data;
  public:
      void updateCache() const { cache = data * 2; }  // allowed due to 'mutable'
  };
  ```

### **Physical vs Logical Const**
* **Physical Const**: Ensures the object's memory representation doesn't change (e.g., getter methods).
* **Logical Const**: From a user's perspective, the object appears unchanged, even if internal, invisible changes occur (e.g., caching).

### **Static Data Members and Member Functions**
* **Static Data Member**: Shared across all instances of the class. Only one copy exists.
  ```cpp
  class MyClass {
  static int sharedVar;
  };
  ```

* **Static Member Function**: Can be called without an instance of the class. Can't access non-static members directly.
  ```cpp
  class MyClass {
  public:
      static void staticFunction();
  };
  ```

### **Operator Overloading**
* Allows custom behavior for C++ operators for user-defined types.
  
  ```cpp
  class Complex {
      double real, imag;
  public:
      Complex operator + (const Complex& obj);
  };
  ```

### **Restrictions in Operator Overloading**
* Can't overload certain operators like `sizeof`, `typeid`.
* No modifying existing operator precedence or associativity.
* Can't introduce new operators.
* Operators `=`, `&`, and `,` are synthesized if not explicitly defined.

### **Key Takeaways**:
* Classes provide a structured way to represent and manage data with behaviors.
* Proper encapsulation ensures code robustness and maintainability.
* Understanding of operator overloading can allow intuitive operations on custom data types.

---

# Chapter 7 : **Class Derivation**

### **Introduction**
* **Class** - A user-defined type that provides an abstraction to a concept by grouping data and linking functionality.

### **Relationships between classes**
1. **Association**
   * **Aggregation** - "X has a Y" relationship.
     * Related objects can exist independently.
     * Weak association.
     * Implemented via reference or shared pointer.
   * **Composition** - "X is part of Y" relationship.
     * Related objects cannot exist independently.
     * Strong association.
     * Implemented as a data member or unique pointer.
   * **Generalization** - "X is a Y" relationship.
     * Implemented via subclassing.

### **Terminology**
* **Superclass** or **Base class** - The primary or main class.
* **Subclass** or **Derived class** - The class that inherits from the Base class.

### **Goals of Class Derivation**
1. **Interface Inheritance** - Different derived classes can be used through the interface of a common base class.
2. **Implementation Reuse** - Derived classes can reuse functionalities from the base class.

### **Member Lookup**
* Process:
   1. Look in the class scope of `this`.
   2. If not found, move up in the inheritance chain.
   3. Stop when the name is found.

### **Access Control**
* **Public members** - Accessible to everyone.
* **Protected members** - Accessible only to subclasses.
* **Private members** - Not accessible to anyone.

### **Data Members in Inheritance**
* Derived class inherits all data members from the base class.
* Can introduce new members in the derived class.
* Cannot access private members of the base class, only public and protected.

### **Memory Layout of a Derived Class**
* Shows how the memory is structured and allocated for base and derived classes.

### **Construction & Destruction**
* **Construction** happens from Base to Derived.
* **Destruction** happens in the reverse order, from Derived to Base.

### **Virtual, Override, and Final**
* **Virtual Function** - Indicates that a derived class can redefine it.
* **Override Function** - Indicates it's virtual and redefines the function from the base class.
* **Final Function** - It's virtual, redefines the base class function, and cannot be overridden by another deriving class.

### **Pure Virtual & Abstract Classes**
* **Pure Virtual Function** - Indicates every derived class must redefine it.
* A class with at least one pure virtual function is termed an **Abstract Class**.
* An **Interface Class** contains only pure virtual functions.

### **Polymorphism**
* A base class pointer can point to an object of a derived class, allowing different classes to be treated as instances of the same class.

### **Vtable**
* A mechanism used to support dynamic dispatch or runtime method binding.
* Each object of a class with virtual functions has a vtable to store addresses of the virtual functions.

### **Virtual Destructor**
* Always make the destructor virtual to prevent memory leaks.

### **Inheritance Design Principles**
* **Liskov Substitution Principle** - Objects of a derived class should be able to replace objects of the base class without affecting correctness.
* **Type Conformity** - Derived classes should respect the base class's conditions and invariants.
* **Principle of Closed Behavior** - Inherited functionalities should respect the derived class’s conditions and invariants.

### **Key Takeaways**:
* Inheritance allows classes to inherit properties and behaviors from other classes.
* Properly leveraging inheritance and polymorphism can lead to efficient and maintainable code structures.
* Adhering to design principles ensures consistency, maintainability, and extensibility in object-oriented programming.

## Chapter 8 : Design Patterns

### Design Principles
- **Liskov Substitution Principle**: Objects of a superclass shall be replaceable with objects of its subclasses without affecting the correctness of the program.
- **Type Conformity**: Ensures that a derived class is compatible with its base class.
- **Principle of Closed Behavior**: Objects should behave as expected when used as instances of a superclass.
- **Single-Responsibility Principle (SRP)**: A class should only have one reason to change, focusing on a single functionality.
- **Open–Closed Principle**: Entities (classes, modules, functions) should be open for extension, but closed for modification.
- **Low Coupling / High Cohesion**: Minimize dependencies between classes (low coupling) and ensure that elements of a class are functionally related (high cohesion).

### Design Patterns Overview
- Design patterns provide tested solutions to common software design issues.
- They adhere to design principles and create a common language for developers.
- Patterns are analyzed based on the problem they solve, their solution, structure, and benefits/drawbacks.

### Creational Patterns
- **Factory Method Pattern**:
  - **Problem**: Creating objects directly within a class using `new` can make the class difficult to extend and maintain.
  - **Solution**: Replace direct construction with calls to a special factory method.
  - **Example (C++)**:
    ```cpp
    class Product {
    public:
        virtual void Operation() = 0;
    };

    class ConcreteProductA : public Product {
    public:
        void Operation() override { /* Implementation */ }
    };

    class Creator {
    public:
        virtual Product* FactoryMethod() = 0;
    };

    class ConcreteCreatorA : public Creator {
    public:
        Product* FactoryMethod() override { return new ConcreteProductA(); }
    };
    ```

- **Abstract Factory Pattern**:
  - **Problem**: Need for creating families of related or dependent objects.
  - **Solution**: Define an interface for creating an object, but let subclasses decide which class to instantiate.
  - **Example (C++)**:
    ```cpp
    class AbstractProductA {
    public:
        virtual void PerformAction() = 0;
    };

    class ConcreteProductA1 : public AbstractProductA {
    public:
        void PerformAction() override { /* Implementation */ }
    };

    class AbstractFactory {
    public:
        virtual AbstractProductA* CreateProductA() = 0;
    };

    class ConcreteFactory1 : public AbstractFactory {
    public:
        AbstractProductA* CreateProductA() override { return new ConcreteProductA1(); }
    };
    ```

### Structural Patterns
- **Adapter Pattern**:
  - **Problem**: Incompatibility between interfaces of different classes.
  - **Solution**: Allows classes with incompatible interfaces to work together by wrapping their interfaces.
  - **Example (C++)**:
    ```cpp
    class Target {
    public:
        virtual void Request() = 0;
    };

    class Adaptee {
    public:
        void SpecificRequest() { /* Specific Implementation */ }
    };

    class Adapter : public Target {
        Adaptee adaptee;
    public:
        void Request() override { adaptee.SpecificRequest(); }
    };
    ```

- **Bridge Pattern**:
  - **Problem**: "Explosion" of classes from combining several dimensions of functionality.
  - **Solution**: Separates an abstraction from its implementation, allowing them to vary independently.
  - **Example (C++)**:
    ```cpp
    class Implementor {
    public:
        virtual void OperationImpl() = 0;
    };

    class ConcreteImplementorA : public Implementor {
    public:
        void OperationImpl() override { /* Implementation */ }
    };

    class Abstraction {
    protected:
        Implementor* implementor;
    public:
        void Operation() { implementor->OperationImpl(); }
    };
    ```

### Behavioral Patterns
- **Command Pattern**:
  - **Problem**: Need to issue requests to objects without knowing anything about the operation being requested or the receiver of the request.
  - **Solution**: Encapsulates a request as an object, thereby allowing for parameterization and queuing of requests.
  - **Example (C++)**:
    ```cpp
    class Command {
    public:
        virtual void Execute() = 0;
    };

    class Receiver {
    public:
        void Action() { /* Specific Action */ }
    };

    class ConcreteCommand : public Command {
        Receiver* receiver;
    public:
        void Execute() override { receiver->Action(); }
    };
    ```

- **Observer Pattern**:
  - **Problem**: One-to-many dependency between objects so that when one object changes state, all its dependents are notified.
  - **Solution**: Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified

 and updated automatically.
  - **Example (C++)**:
    ```cpp
    class Observer {
    public:
        virtual void Update(int state) = 0;
    };

    class Subject {
        std::vector<Observer*> observers;
    public:
        void Attach(Observer* observer) { observers.push_back(observer); }
        void Notify(int state) {
            for (Observer* observer : observers) {
                observer->Update(state);
            }
        }
    };
    ```

### Model-View-Controller (MVC)
- **MVC Pattern**:
  - **Problem**: Managing the UI for an application and keeping the coupling between the front-end and back-end low.
  - **Solution**: Separates an application into three interconnected components: the model, the view, and the controller.
  - **Benefits**: Low coupling, adherence to Single Responsibility Principle, and flexibility to introduce new views or controllers.

### Conclusion
- Design patterns are essential tools for software development, offering solutions to common design problems, ensuring code maintainability, and promoting best practices.
- Understanding and correctly implementing these patterns is crucial for creating robust, scalable, and efficient software.

# Chapter 9: Multi-threading in C++

#### Introduction to Multithreading
- **Multithreading Concept**: Multithreading allows running several threads simultaneously, enhancing performance. A thread is an execution context, containing all information for executing instructions.
- **Real-world Analogy**: Imagine a kitchen in a restaurant as a program. Each chef (thread) works on preparing a different dish (task) simultaneously, leading to faster overall meal preparation (program execution).

#### Using `std::thread`
- **Functionality Assignment**:
  - **Pointer to Function**: Functions reside in memory, and their addresses can be used to execute them.
  - **Lambda Function**: Anonymous functions, useful for concise, temporary functionality.
  
#### Pointer to Function
- **Concept**: Functions can be assigned to pointers for dynamic execution.
- **Example**:
  ```cpp
  void Hello() { std::cout << "Hello, World!\n"; }
  void (*pFunction)() = &Hello; // Assigning function address
  pFunction(); // Calling the function
  ```
  This is like storing a recipe (function) in a cookbook (pointer) and then using the recipe when needed.

#### Lambda Functions
- **Explanation**: Lambdas are quick, anonymous functions defined in-place.
- **Capturing Variables**: Lambdas can 'capture' local variables for use within their scope.
- **Example**:
  ```cpp
  int multiplier = 5;
  auto multiply = [multiplier](int a) { return a * multiplier; };
  std::cout << multiply(3); // Output: 15
  ```
  Think of this like a mini-function where `multiplier` is an ingredient from the shelf (outer scope).

#### Thread Management - Joining and Detaching
- **Joining Threads**: `.join()` makes the main thread wait for the spawned thread to finish.
- **Detaching Threads**: `.detach()` lets the thread run independently, allowing the main thread to continue without waiting.
- **Example**:
  - Joining:
    ```cpp
    std::thread t([]{ std::cout << "Thread running\n"; });
    t.join(); // Main thread waits
    ```
  - Detaching:
    ```cpp
    std::thread t([]{ /* Long running task */ });
    t.detach(); // Main thread doesn't wait
    ```

#### Promise and Future
- **Concept**: Used for transferring a value from one thread to another.
- **Example**:
  ```cpp
  std::promise<int> prom;
  std::future<int> fut = prom.get_future();
  std::thread t([&prom] { prom.set_value(42); });
  std::cout << "Value: " << fut.get(); // Output: 42
  t.join();
  ```
  It's like sending a parcel (value) via a delivery service (promise) and then receiving it (future).

#### Multithreading Challenges - Data Race and Race Conditions
- **Data Race**: Occurs when multiple threads access the same memory location without synchronization.
- **Race Condition**: A bug that appears due to the timing or order of operations.
- **Example of Data Race**:
  ```cpp
  int shared = 0;
  std::thread t1([&]{ shared++; });
  std::thread t2([&]{ shared++; });
  t1.join(); t2.join();
  std::cout << "Shared: " << shared; // Output may vary
  ```
  This is akin to two people writing on the same paper simultaneously, leading to garbled text.

#### Solutions: `std::atomic` and `std::mutex`
- **`std::atomic`**: Makes operations on objects immune to data races.
- **`std::mutex`**: Locks shared data to prevent simultaneous access by multiple threads.
- **Mutex Example**:
  ```cpp
  int shared = 0;
  std::mutex mtx;
  std::thread t1([&]{ std::lock_guard<std::mutex> lock(mtx); shared++; });
  std::thread t2([&]{ std::lock_guard<std::mutex> lock(mtx); shared++; });
  t1.join(); t2.join();
  std::cout << "Shared: " << shared; // Output: 2
  ```
  Imagine a mutex as a key to a room. Only one person (thread) can enter (access the data) at a time.

#### Additional Concepts
- **Deadlocks**: Occurs when two threads are waiting indefinitely for each other to release a resource.
- **Volatile Variables**: Variables that might change unexpectedly, often used in hardware communication.
- **`thread_local` Variables**: Unique to each thread, like having a personal notebook for each chef in the kitchen.

#### Quizzes and Practical Examples
- The chapter includes quizzes and practical code examples, allowing readers to test their understanding of multithreading concepts in a real-world

 context.

#### Conclusion
- Multithreading in C++ is a tool for optimizing performance through parallelism. It requires careful management of threads and resources to avoid common issues like data races and deadlocks. The C++ Standard Library provides various tools like `std::thread`, `std::mutex`, `std::atomic`, `std::promise`, and `std::future` for effective multithreaded programming.

### Chapter 10: Generic Programming 

#### Introduction to Generic Programming
- **Overview**: Generic programming is about creating algorithms and data structures that are abstract and versatile. It's about writing code that can work with a variety of data types.
- **Stroustrup's View**: It's about lifting algorithms from specific instances to their most abstract and reusable form.

#### Templates: The Heart of Generic Programming
- **Role of Templates**: They enable the creation of generic algorithms from concrete ones at compile-time.
- **Concrete vs. Generic Algorithms**: While concrete algorithms work with specific data types, generic algorithms are versatile and can work with any type.

#### Function Templates
- **Concept**: Function templates allow for creating functions without specifying the exact data type.
- **Example**: A function template for comparison:
  ```cpp
  template <typename T>
  bool isEqual(T a, T b) {
      return a == b;
  }
  // Can compare integers, strings, etc.
  ```

#### Template Instantiation
- **Implicit Template Instantiation**: 
  - When you use a template function, the compiler creates a specific version of it for the given type.
  - **Example**: 
    ```cpp
    auto result1 = isEqual<int>(10, 10);  // Instantiates isEqual for int
    auto result2 = isEqual<double>(5.5, 5.5);  // Instantiates isEqual for double
    ```
- **Explicit Template Instantiation**: 
  - You can force the compiler to create a version of the template for a specific type.
  - **Example**: 
    ```cpp
    template bool isEqual<int>(int, int);  // Explicit instantiation for int
    ```

#### Template Argument Deduction
- **Principle**: The compiler deduces the template type from the arguments provided.
- **Explicit Type Specification**: Sometimes, specifying the template type is necessary to avoid ambiguity.

#### Explicit Specialization of a Template Function
- **Overloading Templates**: You can create specialized versions for certain types.
- **Example**: Specializing for `std::string`:
  ```cpp
  template <>
  bool isEqual<std::string>(std::string a, std::string b) {
      return a.compare(b) == 0;
  }
  ```

#### Template Function Overloading
- **Similarity to Regular Functions**: Templates can be overloaded like non-template functions to handle different scenarios.

#### Abbreviated Template Function (C++20)
- **Auto Parameters**: Simplifies template functions using `auto`.
- **Compiler Translation**: Automatically converts them into regular template functions.

#### Auto Keyword (since C++11)
- **Automatic Type Deduction**: `auto` deduces the type of a variable from its initializer, ensuring type correctness and simplifying complex types.

#### Trailing Return Type (since C++11)
- **Usage**: Allows specifying the return type using function parameters and class type aliases.
- **Example**: 
  ```cpp
  template <typename T, typename U>
  auto multiply(T a, U b) -> decltype(a * b) {
      return a * b;
  }
  ```

#### Automatic Return Type Deduction (since C++14)
- **Function Return Types**: The return type of functions can be deduced, removing the need for explicit type declarations.

#### Class Templates
- **Class Template Concept**: Similar to function templates but for classes.
- **Example**:
  ```cpp
  template <typename T>
  class Container {
      T element;
  public:
      Container(T e) : element(e) {}
      T getElement() { return element; }
  };
  ```

#### Class Template Argument Deduction (since C++17)
- **Compiler Assistance**: The compiler can deduce the template arguments for class templates.

#### Default Template Arguments
- **Flexible Templates**: Templates can have default arguments for more versatile use.

#### Class Templates & Inheritance
- **Template vs. Virtual Functions**: Templates provide compile-time polymorphism, while virtual functions offer runtime polymorphism.
- **Virtual Functions in Template Classes**: A template class can contain virtual functions.

#### Universal Reference
- **Concept**: A universal reference can bind to either an lvalue or rvalue reference.
- **Example**:
  ```cpp
  template <typename T>
  void process(T&& arg) {
      // Handle arg as lvalue or rvalue
  }
  ```

#### std::forward (since C++14)
- **Perfect Forwarding**: Preserves the value category (lvalue/rvalue) of arguments, optimizing function calls.

#### Parameter Pack (since C++11)
- **Variadic Templates**: Accepts a variable number of template arguments.
- **Example**: 
  ```cpp
  template <typename... Args>
  void printAll(Args... args) {
      (std::cout << ... << args) << std::endl;
  }
  // Can print any number of arguments


  ```

#### Fold Expressions (since C++17)
- **Parameter Pack Handling**: Simplifies operations on all elements of a parameter pack.
- **Example**: 
  ```cpp
  template<typename... Args>
  auto sum(Args... args) {
      return (args + ...);
  }
  // Sums any number of arguments
  ```

### Conclusion
This detailed overview of generic programming in C++ highlights the versatility and power of templates and features like `auto`, variadic templates, and fold expressions. By understanding these concepts, developers can write more abstract, flexible, and efficient code, suitable for a wide range of types and scenarios. 
