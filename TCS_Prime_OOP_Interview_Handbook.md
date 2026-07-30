# TCS Prime OOP Interview Handbook
### The Complete Object-Oriented Programming Guide for TCS Prime, TCS Digital & TCS Ninja Interviews

*Compiled by a Senior Technical Interviewer — 100 most-asked OOP questions, arranged exactly in the order a real TCS interview flows. Revise this once, the night before your interview.*

---

## Table of Contents

| S.No | Topic | No. of Questions | Difficulty |
|------|-------|-------------------|------------|
| 1 | Introduction to OOP | 8 | Easy |
| 2 | Classes & Objects | 9 | Easy |
| 3 | Constructors & Destructors | 10 | Easy |
| 4 | Access Specifiers | 8 | Easy |
| 5 | Encapsulation | 4 | Medium |
| 6 | Abstraction | 5 | Medium |
| 7 | Inheritance | 5 | Medium |
| 8 | Polymorphism | 5 | Medium |
| 9 | Virtual Functions | 4 | Hard |
| 10 | Function & Operator Overloading | 5 | Medium |
| 11 | Function Overriding | 4 | Medium |
| 12 | Static Members & this Pointer | 5 | Medium |
| 13 | Friend Functions & Friend Classes | 3 | Medium |
| 14 | Memory Management | 5 | Hard |
| 15 | Type Casting | 4 | Hard |
| 16 | Exception Handling | 4 | Medium |
| 17 | Relationships Between Classes | 3 | Hard |
| 18 | SOLID Principles & Design Concepts | 3 | Hard |
| 19 | Scenario-Based Questions | 6 | Hard |
| 20 | Frequently Asked TCS Questions | 30 (bonus rapid-revision set) | Mixed |

**Total core questions: 100** (Easy: 35 · Medium: 40 · Hard: 25)
Topic 20 is a bonus rapid-fire revision list at the very end of this handbook — read it last, 10 minutes before you walk in.

---

# Topic 1: Introduction to OOP

## Question 1

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** What is Object-Oriented Programming?

**Answer**
OOP is a programming paradigm that organizes code around **objects** — real-world entities that bundle data (attributes) and behavior (methods) together. Instead of writing a sequence of instructions like in procedural programming, we model the problem as interacting objects. It is built on four pillars: Encapsulation, Abstraction, Inheritance, and Polymorphism. Languages like C++, Java, and Python support OOP.

---

## Question 2

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** Why do we need OOP? What problem does it solve?

**Answer**
Procedural code becomes hard to manage as projects grow, since data and functions are separate and any function can modify any data. OOP solves this by binding data with the functions that operate on it, so changes stay localized. This gives better **code reusability, security, and scalability**. It also makes large codebases easier to maintain and extend using inheritance and polymorphism.

---

## Question 3

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** What are the main features/pillars of OOP?

**Answer**
The four pillars are: **Encapsulation** (binding data and methods, hiding internal details), **Abstraction** (showing only essential features, hiding complexity), **Inheritance** (reusing properties of one class in another), and **Polymorphism** (one interface, many implementations). Together these make code modular, reusable, and secure.

---

## Question 4

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** What are the advantages of OOP?

**Answer**
OOP gives **code reusability** through inheritance, **data security** through encapsulation, and **flexibility** through polymorphism. It makes large systems easier to **maintain and debug** since related data/logic live in one class. It also supports **modularity**, so teams can work on different classes independently, and models real-world problems more naturally.

---

## Question 5

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** What are the disadvantages/limitations of OOP?

**Answer**
OOP programs can have a **steeper learning curve** and larger design overhead than simple procedural scripts. Excessive use of inheritance can create **tight coupling** between classes, making changes risky. Object-oriented programs are also usually **slower and use more memory** than procedural code because of features like virtual functions and dynamic dispatch. Overengineering small problems with OOP can also add unnecessary complexity.

---

## Question 6

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** Difference between POP (Procedure-Oriented Programming) and OOP?

**Answer**
POP follows a **top-down approach** where the program is divided into functions, and data is global/shared, so it's less secure. OOP follows a **bottom-up approach** where data and functions are combined into objects, giving better security via access specifiers. POP doesn't support inheritance or polymorphism, while OOP does. Example: C is POP, C++/Java are OOP.

---

## Question 7

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** Give a real-world example that explains OOP.

**Answer**
Consider a **Car**: it has attributes (color, model, speed) and behaviors (start, accelerate, brake) — this is a class-object relationship. A **SportsCar** and **SUV** can inherit common properties from a base **Vehicle** class (inheritance). The dashboard shows only "start/stop" buttons, hiding the engine's internal complexity (abstraction). This is exactly how OOP models real systems.

---

## Question 8

**Topic:** Introduction to OOP

**Difficulty:** Easy

**Interview Question:** Where is OOP used in real applications?

**Answer**
OOP is used in **GUI applications**, **game development**, **enterprise software** (banking, ERP systems), **mobile apps** (Android is Java/Kotlin-based OOP), and **frameworks** like Spring and .NET. Any large system that needs modular, reusable, and maintainable code — like TCS's own client projects — is typically built using OOP principles.

---

# Topic 2: Classes & Objects

## Question 9

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What is a class?

**Answer**
A class is a **user-defined blueprint or template** that defines what data (member variables) and behavior (member functions) its objects will have. No memory is allocated when a class is declared — it's just a design. Example: `class Car { string color; void start(); };` defines the structure, not an actual car.

---

## Question 10

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What is an object?

**Answer**
An object is a **real instance of a class** — memory is allocated for it, and it holds actual values for the class's data members. Multiple objects can be created from one class, each with its own copy of data (except static members). Example: `Car myCar;` creates an object `myCar` from the `Car` class.

---

## Question 11

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** Class vs Object — what's the difference?

**Answer**
A **class** is a logical blueprint with no memory allocated; an **object** is a physical instance with memory allocated. A class is declared once, but many objects can be created from it. Class defines *what properties will exist*; object holds the *actual values*. Analogy: "House blueprint" is the class, and each constructed house is an object.

---

## Question 12

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What are data members and member functions?

**Answer**
**Data members** are the variables declared inside a class that store an object's state (e.g., `name`, `age`). **Member functions** are the methods defined inside a class that operate on that data (e.g., `getAge()`, `setName()`). Together they implement encapsulation — the data and the logic that manipulates it live in one place.

---

## Question 13

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What happens in memory when an object is created?

**Answer**
When an object is created, memory is allocated on the **stack** (for local objects) or **heap** (if created with `new`) to store its non-static data members. Member functions are **not duplicated per object** — only one copy exists in code memory, and it is shared by all objects, invoked using the hidden `this` pointer for the calling object.

---

## Question 14

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** How do you access members of a class through an object?

**Answer**
Public members are accessed using the **dot (`.`) operator** on an object, like `obj.name` or `obj.display()`. If you have a **pointer to an object**, you use the **arrow (`->`) operator**, like `ptr->display()`. Private/protected members can't be accessed directly from outside — only through public getter/setter functions.

---

## Question 15

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What is the Scope Resolution Operator (`::`) used for?

**Answer**
The `::` operator is used to **define a member function outside the class body** while still linking it to the class, e.g., `void Car::start() { ... }`. It's also used to access a **static member**, a **global variable** shadowed by a local one, or a specific class's version of a member in multiple inheritance.

---

## Question 16

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What is an inline function and why use it in a class?

**Answer**
An inline function is one where the compiler **replaces the function call with the actual function code** at compile time, to avoid function-call overhead. Functions defined **inside a class body are inline by default**. It's useful for small, frequently-called functions like getters/setters, but overusing it on large functions increases binary size.

---

## Question 17

**Topic:** Classes & Objects

**Difficulty:** Easy

**Interview Question:** What is a namespace and why is it used?

**Answer**
A namespace is a **named scope** that groups classes, functions, and variables to avoid naming conflicts, especially when using multiple libraries. For example, `std::cout` tells the compiler `cout` belongs to the `std` namespace. It keeps large codebases organized and prevents clashes between identically-named identifiers from different modules.

---

# Topic 3: Constructors & Destructors

## Question 18

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is a constructor?

**Answer**
A constructor is a **special member function** that is automatically called when an object is created, used to initialize its data members. It has the **same name as the class**, has **no return type** (not even `void`), and can be overloaded. If you don't write one, the compiler generates a default constructor for you.

---

## Question 19

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is a default constructor?

**Answer**
A default constructor is a constructor that **takes no parameters** (or has default values for all parameters). It initializes data members to default values, like 0 or empty strings. If a class has no constructor at all, the compiler auto-generates an empty default constructor — but this is skipped if you define any other constructor yourself.

---

## Question 20

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is a parameterized constructor?

**Answer**
A parameterized constructor accepts **arguments** so an object can be initialized with specific values at creation time, e.g., `Car(string c) { color = c; }`. This avoids the need to set values separately after object creation. A class can have multiple parameterized constructors through constructor overloading.

---

## Question 21

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is a copy constructor?

**Answer**
A copy constructor creates a **new object as a copy of an existing object** of the same class, e.g., `Car c2(c1);`. Its signature takes a reference to the same class type: `Car(const Car &obj)`. If not defined explicitly, the compiler provides a default one that does a **shallow copy**, member by member.

---

## Question 22

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is constructor overloading?

**Answer**
Constructor overloading means defining **multiple constructors with different parameter lists** in the same class, so objects can be initialized in different ways. The compiler picks the right one based on the arguments passed during object creation. Example: having both `Car()` and `Car(string color)` in the same class.

---

## Question 23

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is constructor chaining?

**Answer**
Constructor chaining is calling **one constructor from another** to avoid duplicating initialization code. Within the same class, this is done using an initializer list, e.g., `Car() : Car("Red") {}`. In inheritance, chaining refers to a derived class constructor implicitly or explicitly calling the base class constructor before running its own body.

---

## Question 24

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is a destructor?

**Answer**
A destructor is a special member function that is **automatically called when an object goes out of scope or is deleted**, used to release resources like memory, file handles, or network connections. It has the same name as the class prefixed with `~`, takes **no parameters**, has **no return type**, and cannot be overloaded — a class has only one destructor.

---

## Question 25

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** Constructor vs Destructor — what's the difference?

**Answer**
A **constructor** initializes an object and is called when it's **created**; a **destructor** cleans up resources and is called when it's **destroyed**. Constructors can be **overloaded** and take parameters; destructors take **no parameters** and cannot be overloaded. Naming: constructor = `ClassName()`, destructor = `~ClassName()`.

---

## Question 26

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is the order of constructor and destructor calls in inheritance?

**Answer**
Constructors are called in the order of inheritance — **base class constructor runs first, then the derived class constructor** — because a derived object needs its base part built first. Destructors run in the **exact reverse order** — derived class destructor first, then base class destructor — since the derived part must be cleaned up before the base part.

---

## Question 27

**Topic:** Constructors & Destructors

**Difficulty:** Easy

**Interview Question:** What is a copy assignment operator, and how is it different from a copy constructor?

**Answer**
The copy assignment operator (`operator=`) copies values from one **already existing** object to another, e.g., `c2 = c1;`, whereas the **copy constructor** initializes a **brand-new** object from an existing one, e.g., `Car c2 = c1;`. If not user-defined, the compiler auto-generates both, doing a member-wise (shallow) copy, which is unsafe for classes holding raw pointers.

---

# Topic 4: Access Specifiers

## Question 28

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** What is the `public` access specifier?

**Answer**
Members declared `public` can be accessed from **anywhere** — inside the class, by derived classes, and from outside code using an object. It's used for the class's interface — methods meant to be called by other parts of the program, like `getName()` or `deposit()`.

---

## Question 29

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** What is the `private` access specifier?

**Answer**
Members declared `private` can be accessed **only within the same class** — not by derived classes and not from outside. This is the default access level for a `class` in C++. It's the main mechanism for **data hiding**; you expose controlled access through public getter/setter methods instead.

---

## Question 30

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** What is the `protected` access specifier?

**Answer**
`protected` members behave like `private` for the outside world — inaccessible directly — but unlike `private`, they **are accessible inside derived classes**. It's used when you want child classes to reuse a base class's internal data directly, without exposing it publicly to the rest of the program.

---

## Question 31

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** Summarize the accessibility of public, private, and protected members.

**Answer**
| Access | Same Class | Derived Class | Outside Class |
|---|---|---|---|
| public | Yes | Yes | Yes |
| protected | Yes | Yes | No |
| private | Yes | No | No |

This table is a favorite quick-fire TCS question — memorize it exactly.

---

## Question 32

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** What happens to base class members under **public inheritance**?

**Answer**
Under public inheritance, the base class's `public` members **stay public** and `protected` members **stay protected** in the derived class; `private` members remain **inaccessible** directly in the derived class. Public inheritance is the most common form and represents a true **IS-A relationship**.

---

## Question 33

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** What happens under **protected** and **private** inheritance?

**Answer**
Under **protected inheritance**, base `public` and `protected` members both become `protected` in the derived class. Under **private inheritance**, base `public` and `protected` members both become `private` in the derived class — so they aren't accessible even to classes derived further down. Private members of the base always stay inaccessible regardless of inheritance type.

---

## Question 34

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** How does a `friend` function affect access specifiers?

**Answer**
A `friend` function or class is granted access to a class's `private` and `protected` members **even though it isn't a member** of that class. It's declared inside the class with the `friend` keyword. It breaks strict encapsulation slightly but is useful for operator overloading (like overloading `<<` for `cout`) or tightly coupled helper classes.

---

## Question 35

**Topic:** Access Specifiers

**Difficulty:** Easy

**Interview Question:** What is the default access specifier for `class` vs `struct`?

**Answer**
In C++, members and inheritance are **`private` by default in a `class`**, but **`public` by default in a `struct`**. This is actually the only functional difference between `class` and `struct` in C++ — everything else (methods, constructors, inheritance) works identically for both.

---

# Topic 5: Encapsulation

## Question 36

**Topic:** Encapsulation

**Difficulty:** Medium

**Interview Question:** What is encapsulation?

**Answer**
Encapsulation is the process of **binding data and the functions that operate on it into a single unit** (a class), while restricting direct access to the internal data. It's implemented using access specifiers — keeping data `private` and exposing controlled access via `public` getter/setter methods. It's often described as "data hiding with controlled access."

---

## Question 37

**Topic:** Encapsulation

**Difficulty:** Medium

**Interview Question:** What are the benefits of encapsulation?

**Answer**
Encapsulation gives **data security**, since internal state can't be modified directly or invalidly from outside. It allows you to **change internal implementation** without breaking external code, as long as the public interface stays the same. It also improves **maintainability** and enables **validation logic** inside setters, e.g., rejecting a negative age.

---

## Question 38

**Topic:** Encapsulation

**Difficulty:** Medium

**Interview Question:** Give a real-world example of encapsulation.

**Answer**
A **capsule/medicine tablet** hides its internal chemical composition inside an outer coating — you just consume it without needing to know what's inside. Similarly, a **bank account class** hides the `balance` variable as private, and you can only change it through controlled methods like `deposit()` and `withdraw()`, which can enforce rules like "balance cannot go negative."

---

## Question 39

**Topic:** Encapsulation

**Difficulty:** Medium

**Interview Question:** Why do we use getter and setter methods instead of making variables public directly?

**Answer**
Getters and setters let you **add validation** before changing data — for example, a setter can reject a negative salary or an invalid email format, which a plain public variable can't do. It also gives you the flexibility to **change internal representation later** (e.g., switching from `int age` to computing age from `DOB`) without changing how external code calls `getAge()`.

---

# Topic 6: Abstraction

## Question 40

**Topic:** Abstraction

**Difficulty:** Medium

**Interview Question:** What is abstraction?

**Answer**
Abstraction means **showing only the essential features** of an object while **hiding the internal implementation details**. The user interacts with a simple interface without needing to know the complex logic behind it. In OOP, it's achieved using **abstract classes** and **interfaces**, which define *what* a class should do, not *how*.

---

## Question 41

**Topic:** Abstraction

**Difficulty:** Medium

**Interview Question:** What is an abstract class and a pure virtual function?

**Answer**
An abstract class is a class that **cannot be instantiated directly** and contains at least one **pure virtual function** — a virtual function with no body, declared as `virtual void draw() = 0;`. It acts as a template that forces every derived class to provide its own implementation of that function. It can still have regular member functions and data with implementations.

---

## Question 42

**Topic:** Abstraction

**Difficulty:** Medium

**Interview Question:** What is an interface in OOP?

**Answer**
An interface is a **fully abstract type** that only declares method signatures with no implementation at all, forcing every implementing class to define all of them. In C++, there's no dedicated `interface` keyword, so it's simulated using a class with **only pure virtual functions**. In Java/C#, `interface` is a built-in keyword for this exact purpose.

---

## Question 43

**Topic:** Abstraction

**Difficulty:** Medium

**Interview Question:** Abstract Class vs Interface — what's the difference?

**Answer**
An **abstract class** can have a mix of implemented methods and pure virtual (abstract) methods, plus data members and constructors. An **interface** has **only method declarations**, no implementation and no state (in languages that support it as a keyword). A class can inherit from only **one** abstract class typically, but can implement **multiple** interfaces.

---

## Question 44

**Topic:** Abstraction

**Difficulty:** Medium

**Interview Question:** Abstraction vs Encapsulation — what's the difference?

**Answer**
**Abstraction** hides **complexity** by showing only relevant details — it's a **design-level** concept (what to show). **Encapsulation** hides **data** by restricting direct access — it's an **implementation-level** concept (how to protect). Analogy: a car's steering wheel is abstraction (you just drive), while the engine sealed under the hood is encapsulation (you can't touch it directly).

---

# Topic 7: Inheritance

## Question 45

**Topic:** Inheritance

**Difficulty:** Medium

**Interview Question:** What is inheritance and what are its benefits?

**Answer**
Inheritance lets a **derived (child) class** acquire the properties and behaviors of a **base (parent) class**, using the syntax `class Derived : public Base`. It gives **code reusability** (no need to rewrite common logic), supports **extensibility** (add new features in the child class), and models real **IS-A relationships**, like `Dog IS-A Animal`.

---

## Question 46

**Topic:** Inheritance

**Difficulty:** Medium

**Interview Question:** What are the types of inheritance?

**Answer**
There are five types: **Single** (one base, one derived), **Multiple** (one derived from two or more base classes), **Multilevel** (a chain — A → B → C), **Hierarchical** (multiple derived classes from one base), and **Hybrid** (a combination of the above, e.g., hierarchical + multiple). Java doesn't support multiple inheritance of classes directly, but C++ does.

---

## Question 47

**Topic:** Inheritance

**Difficulty:** Medium

**Interview Question:** In what order are constructors called when using multilevel inheritance?

**Answer**
Constructors always run **from the topmost base class down to the most derived class**. So for `A → B → C`, the order is `A()`, then `B()`, then `C()`. This ensures each layer of the object is fully initialized before the next layer builds on top of it. Destructors run in the exact reverse order.

---

## Question 48

**Topic:** Inheritance

**Difficulty:** Medium

**Interview Question:** What is the Diamond Problem in inheritance?

**Answer**
The Diamond Problem occurs in **multiple inheritance** when two classes `B` and `C` both inherit from the same class `A`, and a class `D` inherits from both `B` and `C`. This creates **two copies of `A`'s members inside `D`**, causing ambiguity about which copy to use. It's called "diamond" because the class hierarchy diagram looks like a diamond shape.

---

## Question 49

**Topic:** Inheritance

**Difficulty:** Medium

**Interview Question:** How is the Diamond Problem solved? Give a real-world example.

**Answer**
C++ solves it using **virtual inheritance** — declaring `class B : virtual public A` ensures only **one shared copy** of `A` exists in `D`, removing the ambiguity. Real-world example: a `SmartPhone` class inheriting from both `Camera` and `Phone`, which both inherit from a common `Device` class — without virtual inheritance, `SmartPhone` would get two ambiguous copies of `Device`.

---

# Topic 8: Polymorphism

## Question 50

**Topic:** Polymorphism

**Difficulty:** Medium

**Interview Question:** Compile-time vs Runtime Polymorphism — what's the difference?

**Answer**
**Compile-time polymorphism** (also called static polymorphism) is resolved by the compiler **before execution**, achieved via **function overloading** and **operator overloading**. **Runtime polymorphism** (dynamic polymorphism) is resolved **during execution**, achieved via **function overriding** with **virtual functions**. Compile-time is faster (no lookup overhead); runtime is more flexible (decided based on actual object type).

---

## Question 51

**Topic:** Polymorphism

**Difficulty:** Medium

**Interview Question:** What is static binding?

**Answer**
Static binding (early binding) means the compiler decides **at compile time** which function to call, based on the **static type** of the pointer/reference or the function signature. It's used in normal function calls, function overloading, and non-virtual member functions. It's faster since there's no runtime lookup involved.

---

## Question 52

**Topic:** Polymorphism

**Difficulty:** Medium

**Interview Question:** What is dynamic binding? Static Binding vs Dynamic Binding — what's the difference?

**Answer**
Dynamic binding (late binding) means the function call is resolved **at runtime**, based on the **actual object type**, not the pointer/reference type — this happens with **virtual functions**. Static binding is resolved at **compile time** and is faster; dynamic binding is resolved at **runtime** using the vtable and enables true runtime polymorphism, at a small performance cost.

---

## Question 53

**Topic:** Polymorphism

**Difficulty:** Medium

**Interview Question:** What are the benefits of polymorphism?

**Answer**
Polymorphism lets you write **generic code** that works with objects of different derived types through a common base class interface, e.g., a single `draw()` call working correctly for `Circle`, `Square`, or `Triangle`. This improves **code flexibility, extensibility** (add new derived classes without touching existing code), and supports patterns like the Strategy or Factory pattern.

---

## Question 54

**Topic:** Polymorphism

**Difficulty:** Medium

**Interview Question:** Give a real-world example of polymorphism, and explain object slicing.

**Answer**
A common example: pressing "print" behaves differently for a PDF, image, or text file, but the interface (`print()`) is the same — that's polymorphism. **Object slicing** is a related pitfall: if you assign a derived class object to a **base class object (not pointer/reference)**, the derived part gets "sliced off," and only the base part is copied — so always use pointers or references for polymorphic behavior.

---

# Topic 9: Virtual Functions

## Question 55

**Topic:** Virtual Functions

**Difficulty:** Hard

**Interview Question:** What is a virtual function and why do we need it?

**Answer**
A virtual function is a member function declared in the base class with the `virtual` keyword, which can be **overridden in a derived class**, and is resolved using **dynamic binding** based on the actual object type. It's needed to achieve **runtime polymorphism** — without it, calling a function through a base class pointer would always call the base version, even if the object is actually derived.

---

## Question 56

**Topic:** Virtual Functions

**Difficulty:** Hard

**Interview Question:** What is a virtual destructor and why is it important?

**Answer**
A virtual destructor ensures that when you `delete` an object **through a base class pointer**, the **derived class's destructor runs first**, followed by the base's — properly releasing all resources. Without it, only the base destructor runs, causing a **memory leak** for any resources the derived class allocated. Rule of thumb: if a class has any virtual function, its destructor should be virtual too.

---

## Question 57

**Topic:** Virtual Functions

**Difficulty:** Hard

**Interview Question:** What are vtable and vptr? How does dynamic dispatch work?

**Answer**
The **vtable (virtual table)** is a hidden array of function pointers that the compiler creates **per class** that has virtual functions, storing addresses of the actual functions to call. Every object of such a class has a hidden **vptr (virtual pointer)** that points to its class's vtable. At runtime, a virtual call looks up the vptr → vtable → correct function address — this lookup mechanism is called **dynamic dispatch**.

---

## Question 58

**Topic:** Virtual Functions

**Difficulty:** Hard

**Interview Question:** Virtual Function vs Pure Virtual Function — what's the difference?

**Answer**
A **virtual function** has a **default implementation** in the base class, which a derived class **may optionally override**. A **pure virtual function** (`= 0`) has **no implementation** in the base class, and **must be overridden** by any concrete derived class. A class with even one pure virtual function becomes an **abstract class** and cannot be instantiated.

---

# Topic 10: Function & Operator Overloading

## Question 59

**Topic:** Function & Operator Overloading

**Difficulty:** Medium

**Interview Question:** What is function overloading? What are the rules?

**Answer**
Function overloading means having **multiple functions with the same name** in the same scope, differentiated by their **parameter list** — different number, type, or order of parameters. Return type alone **cannot** differentiate overloads. The compiler picks the correct version at compile time based on the arguments passed, so it's a form of **compile-time polymorphism**.

---

## Question 60

**Topic:** Function & Operator Overloading

**Difficulty:** Medium

**Interview Question:** What are the advantages and limitations of function overloading?

**Answer**
Advantages: it improves **readability** by using one intuitive name for related actions (e.g., `add(int,int)` and `add(float,float)`), and increases code clarity. Limitation: overloading based only on **return type isn't allowed**, and too many overloads for slightly different behaviors can confuse readers and cause ambiguity errors if the compiler can't uniquely resolve a call.

---

## Question 61

**Topic:** Function & Operator Overloading

**Difficulty:** Medium

**Interview Question:** What is operator overloading? Give the syntax.

**Answer**
Operator overloading lets you **redefine how an operator behaves for user-defined types** (classes), so objects can use natural syntax like `+` or `==`. Syntax: `ReturnType operator+(const ClassName &obj) { ... }`. Example: overloading `+` for a `Complex` class so `c3 = c1 + c2` adds real and imaginary parts correctly.

---

## Question 62

**Topic:** Function & Operator Overloading

**Difficulty:** Medium

**Interview Question:** What are the rules for operator overloading?

**Answer**
You **cannot create new operators** or change an operator's precedence/associativity. Operators like `::`, `.`, `.*`, `?:`, and `sizeof` **cannot be overloaded**. At least one operand must be a **user-defined type** (you can't overload `+` for two built-in `int`s). It should also make logical sense — overloading `+` to perform subtraction would be confusing and bad practice.

---

## Question 63

**Topic:** Function & Operator Overloading

**Difficulty:** Medium

**Interview Question:** What are the limitations of operator overloading?

**Answer**
It can be **misused** to make code confusing if the overloaded behavior doesn't match the operator's natural meaning. Some operators (like `=`, `[]`, `()`, `->`) **must be overloaded as member functions**, not as free/friend functions, which adds design constraints. It also adds a small amount of function-call overhead compared to using built-in operators directly.

---

# Topic 11: Function Overriding

## Question 64

**Topic:** Function Overriding

**Difficulty:** Medium

**Interview Question:** What is function/method overriding?

**Answer**
Overriding happens when a **derived class provides its own implementation** of a function that already exists in its base class, using the **same name, same parameters, and same return type**. It requires the base function to be marked `virtual` for the override to work polymorphically through a base pointer/reference. This is how **runtime polymorphism** is achieved.

---

## Question 65

**Topic:** Function Overriding

**Difficulty:** Medium

**Interview Question:** What are the rules for overriding, and what does the `override` keyword do?

**Answer**
The overriding function must have the **exact same signature** (name, parameters, and const-ness) as the base version, and the base function must be `virtual`. The `override` keyword (C++11+) is added in the derived class to explicitly tell the compiler "this should override a base virtual function" — if it doesn't actually match, you get a **compile error** instead of a silent bug.

---

## Question 66

**Topic:** Function Overriding

**Difficulty:** Medium

**Interview Question:** Overloading vs Overriding — what's the difference?

**Answer**
**Overloading** happens **within the same class** (or scope) with **different parameter lists** and is resolved at **compile time**. **Overriding** happens **between a base and derived class** with the **same signature** and is resolved at **runtime** using virtual functions. Overloading = compile-time polymorphism; Overriding = runtime polymorphism. This is one of the most frequently asked TCS comparison questions.

---

## Question 67

**Topic:** Function Overriding

**Difficulty:** Medium

**Interview Question:** Why is overriding important in large applications?

**Answer**
Overriding lets a program treat different derived objects **uniformly through a base class interface**, while each object still executes its **own specific behavior**. For example, a `PaymentGateway` base class with an overridden `pay()` method lets `CreditCardPayment` and `UPIPayment` plug in seamlessly, so you can add new payment types **without modifying existing calling code** — this is the Open/Closed Principle in action.

---

# Topic 12: Static Members & this Pointer

## Question 68

**Topic:** Static Members & this Pointer

**Difficulty:** Medium

**Interview Question:** What is a static variable in a class?

**Answer**
A static variable is **shared by all objects** of the class — there's only **one copy** in memory regardless of how many objects are created, unlike normal data members which get a separate copy per object. It must be **defined outside the class** (in C++) to allocate storage, e.g., `int Car::count = 0;`. It's commonly used to count how many objects have been created.

---

## Question 69

**Topic:** Static Members & this Pointer

**Difficulty:** Medium

**Interview Question:** What is a static member function?

**Answer**
A static member function **belongs to the class, not to any specific object**, so it can be called using the class name directly, like `Car::getCount()`. It can only access **static data members** and other static functions — it has **no `this` pointer**, so it cannot access non-static (instance) members directly.

---

## Question 70

**Topic:** Static Members & this Pointer

**Difficulty:** Medium

**Interview Question:** What is a static object, and what is the lifetime/memory allocation of static members?

**Answer**
A static object is an object declared with the `static` keyword inside a function or class, meaning it's **created only once** and retains its value across multiple calls, rather than being recreated each time. Static members (variables) are stored in a fixed area of memory (**data segment**, not stack/heap) and exist for the **entire duration of the program**, being initialized once before `main()` runs.

---

## Question 71

**Topic:** Static Members & this Pointer

**Difficulty:** Medium

**Interview Question:** What is the `this` pointer and where is it used?

**Answer**
`this` is an **implicit pointer** available inside every non-static member function, pointing to the **object that invoked the function**. It's used to resolve naming conflicts between a parameter and a data member (e.g., `this->name = name;`), to return the current object from a member function, and to pass the current object to another function.

---

## Question 72

**Topic:** Static Members & this Pointer

**Difficulty:** Medium

**Interview Question:** What is method chaining, and how does returning `*this` enable it?

**Answer**
Method chaining lets you call multiple member functions on the same object in a single statement, like `obj.setName("A").setAge(20);`. This works because each setter function **returns `*this`** — a reference to the current object — so the next method call can immediately be applied on the same object. It results in cleaner, more fluent code, commonly seen in builder-pattern designs.

---

# Topic 13: Friend Functions & Friend Classes

## Question 73

**Topic:** Friend Functions & Friend Classes

**Difficulty:** Medium

**Interview Question:** What is a friend function?

**Answer**
A friend function is a **non-member function** that is granted access to a class's `private` and `protected` members, by declaring it inside the class with the `friend` keyword. It's commonly used to overload operators like `<<` for printing objects with `cout`, where the function needs access to private data but can't be a member function of the class due to operand order.

---

## Question 74

**Topic:** Friend Functions & Friend Classes

**Difficulty:** Medium

**Interview Question:** What is a friend class? What are the advantages and limitations?

**Answer**
A friend class is a class that is given access to another class's `private` and `protected` members, declared as `friend class OtherClass;`. It's useful when two classes are **tightly coupled** and need deep access to each other, like a `LinkedList` and its `Iterator`. The main limitation is that it **breaks strict encapsulation**, so it should be used sparingly and only when truly needed.

---

## Question 75

**Topic:** Friend Functions & Friend Classes

**Difficulty:** Medium

**Interview Question:** Friend Function vs Member Function — what's the difference?

**Answer**
A **member function** is called using an object with the dot operator (`obj.func()`) and has an implicit `this` pointer. A **friend function** is called like a normal function (`func(obj)`), is **not a member**, has **no `this` pointer**, but can still access the class's private/protected data because it's explicitly granted friendship. Friendship is **not mutual or inherited** — it must be declared explicitly on each side.

---

# Topic 14: Memory Management

## Question 76

**Topic:** Memory Management

**Difficulty:** Hard

**Interview Question:** Stack vs Heap — what's the difference?

**Answer**
The **stack** stores local variables and function call data, is managed **automatically** by the compiler (allocated/deallocated as functions are entered/exited), is faster, but limited in size. The **heap** is used for **dynamic memory allocation** (`new`/`malloc`), managed **manually** by the programmer, is larger, but slower and prone to memory leaks if not freed with `delete`/`free`.

---

## Question 77

**Topic:** Memory Management

**Difficulty:** Hard

**Interview Question:** How do `new` and `delete` work for dynamic memory allocation?

**Answer**
`new` allocates memory **on the heap** for an object and returns a pointer to it, also calling the object's constructor, e.g., `Car *c = new Car();`. `delete` frees that memory and calls the destructor, e.g., `delete c;`. For arrays, use `new[]` and `delete[]` together — mismatching them (e.g., `delete` on a `new[]`) causes **undefined behavior**.

---

## Question 78

**Topic:** Memory Management

**Difficulty:** Hard

**Interview Question:** What is a memory leak and a dangling pointer?

**Answer**
A **memory leak** happens when dynamically allocated memory is **never freed** (no `delete` called) and becomes unreachable, wasting memory over the program's lifetime. A **dangling pointer** is a pointer that still points to memory that has **already been freed** (`delete`d) — using it afterward causes undefined behavior. Setting a pointer to `nullptr` right after `delete` helps avoid dangling pointer bugs.

---

## Question 79

**Topic:** Memory Management

**Difficulty:** Hard

**Interview Question:** Deep Copy vs Shallow Copy — what's the difference?

**Answer**
A **shallow copy** copies the values of data members as-is — if a member is a pointer, only the **address is copied**, so both objects end up pointing to the **same memory** (dangerous, causes double-free bugs). A **deep copy** creates a **completely independent copy** of any dynamically allocated data, so each object has its own memory. The compiler's default copy constructor does a shallow copy — for classes with pointers, you must write a custom deep-copy constructor.

---

## Question 80

**Topic:** Memory Management

**Difficulty:** Hard

**Interview Question:** What is a smart pointer, and what is RAII?

**Answer**
A smart pointer (like `unique_ptr` or `shared_ptr` in C++) is a class that **wraps a raw pointer** and automatically calls `delete` when it goes out of scope, preventing memory leaks. This is an application of **RAII (Resource Acquisition Is Initialization)** — the principle that a resource's lifetime should be tied to an object's lifetime, so it's acquired in the constructor and automatically released in the destructor.

---

# Topic 15: Type Casting

## Question 81

**Topic:** Type Casting

**Difficulty:** Hard

**Interview Question:** Implicit vs Explicit type conversion — what's the difference?

**Answer**
**Implicit conversion** is done **automatically by the compiler** when types are compatible, e.g., assigning an `int` to a `double`. **Explicit conversion (casting)** is done **manually by the programmer** using cast operators when the compiler won't convert automatically, or when you want to force a conversion, e.g., `(int)3.14` or `static_cast<int>(3.14)`. Explicit casting gives the programmer more control and clarity about intent.

---

## Question 82

**Topic:** Type Casting

**Difficulty:** Hard

**Interview Question:** static_cast vs dynamic_cast — what's the difference?

**Answer**
`static_cast` is resolved at **compile time**, is faster, but does **no runtime safety check** — used for well-defined conversions like `int` to `float` or upcasting. `dynamic_cast` is resolved at **runtime**, used mainly for **safe downcasting** in polymorphic class hierarchies, and returns `nullptr` (for pointers) if the cast is invalid — but it **requires the base class to have at least one virtual function** (a vtable) to work.

---

## Question 83

**Topic:** Type Casting

**Difficulty:** Hard

**Interview Question:** What are const_cast and reinterpret_cast used for?

**Answer**
`const_cast` is used to **add or remove `const`/`volatile`** qualifiers from a variable — for example, passing a `const` object to a function that isn't `const`-correct. `reinterpret_cast` performs a **low-level, unsafe reinterpretation** of a pointer's bit pattern as a different, often unrelated type, e.g., converting a pointer to an integer. Both should be used **rarely and carefully**, as misuse can cause undefined behavior.

---

## Question 84

**Topic:** Type Casting

**Difficulty:** Hard

**Interview Question:** Upcasting vs Downcasting — what's the difference?

**Answer**
**Upcasting** converts a **derived class pointer/reference to a base class type** — it's always safe and often done implicitly, since a derived object always "IS-A" base object. **Downcasting** converts a **base class pointer/reference back to a derived type** — it's riskier since the base pointer might not actually point to that derived type, so it should use `dynamic_cast` to safely check and avoid undefined behavior.

---

# Topic 16: Exception Handling

## Question 85

**Topic:** Exception Handling

**Difficulty:** Medium

**Interview Question:** What are try, catch, and throw?

**Answer**
`try` defines a block of code that might raise an error, which is **monitored for exceptions**. `throw` is used to **signal that an error has occurred**, sending an exception object. `catch` **handles** the exception that was thrown, matching it by type, e.g., `catch (std::exception &e) { ... }`. Together they let a program handle runtime errors gracefully instead of crashing.

---

## Question 86

**Topic:** Exception Handling

**Difficulty:** Medium

**Interview Question:** What are multiple catch blocks and nested try-catch?

**Answer**
**Multiple catch blocks** let you handle **different exception types differently** after a single `try` block, e.g., separate `catch` blocks for `DivideByZeroException` and `FileNotFoundException`. **Nested try-catch** means placing a `try-catch` block **inside another try or catch block**, useful when an inner operation needs its own specific error handling before the outer block handles broader issues.

---

## Question 87

**Topic:** Exception Handling

**Difficulty:** Medium

**Interview Question:** What are exception specifications and best practices for exception handling?

**Answer**
Exception specifications (like the older `throw()` keyword, now replaced by `noexcept` in modern C++) declare what exceptions a function might throw, helping callers handle them correctly. Best practices: **catch exceptions by reference** (not by value, to avoid slicing), only catch exceptions you can **meaningfully handle**, always **release resources** (use RAII/smart pointers) so exceptions don't cause leaks, and avoid using exceptions for normal control flow.

---

## Question 88

**Topic:** Exception Handling

**Difficulty:** Medium

**Interview Question:** What happens if a constructor throws an exception?

**Answer**
If a constructor throws, the object is considered to have **never been fully constructed**, so its destructor is **never called**. However, any **fully-constructed sub-objects or base classes** built before the exception will have their destructors called automatically, to avoid leaking those parts. This is why RAII and smart pointers inside constructors are important — they clean up safely even if construction fails partway.

---

# Topic 17: Relationships Between Classes

## Question 89

**Topic:** Relationships Between Classes

**Difficulty:** Hard

**Interview Question:** What are Association, Aggregation, and Composition?

**Answer**
**Association** is a general relationship where two classes are related but exist **independently** of each other, e.g., a `Teacher` and a `Student`. **Aggregation** is a special "HAS-A" association where one object **contains** another, but the contained object **can exist independently** (weak ownership), e.g., a `Department` has `Professors`, but professors exist even if the department closes. **Composition** is a stronger "HAS-A" where the contained object **cannot exist without the owner** (strong ownership), e.g., a `House` has `Rooms` — destroy the house, and the rooms are destroyed too.

---

## Question 90

**Topic:** Relationships Between Classes

**Difficulty:** Hard

**Interview Question:** Aggregation vs Composition — what's the difference?

**Answer**
In **aggregation**, the "part" object can **exist independently** of the "whole" — it's a **weak** relationship (shared/loose ownership), e.g., a `Library` and its `Books` (books can exist without that specific library). In **composition**, the "part" **cannot exist independently** of the "whole" — it's a **strong** relationship (exclusive ownership) with matching lifetimes, e.g., an `Engine` inside a `Car` — the engine is created and destroyed with the car.

---

## Question 91

**Topic:** Relationships Between Classes

**Difficulty:** Hard

**Interview Question:** IS-A vs HAS-A relationship — what's the difference?

**Answer**
**IS-A** represents **inheritance** — a derived class is a specialized type of its base class, e.g., `Dog IS-A Animal`, implemented using `class Dog : public Animal`. **HAS-A** represents **composition/aggregation** — a class contains another class as a member, e.g., `Car HAS-A Engine`, implemented by having an `Engine` object as a data member inside `Car`. Interviewers often ask: "when would you prefer HAS-A over IS-A?" — answer: when the relationship isn't truly a specialization, to avoid fragile deep inheritance hierarchies.

---

# Topic 18: SOLID Principles & Design Concepts

## Question 92

**Topic:** SOLID Principles & Design Concepts

**Difficulty:** Hard

**Interview Question:** Explain the Single Responsibility Principle (SRP) and Open/Closed Principle (OCP) with examples.

**Answer**
**SRP**: a class should have **only one reason to change** — one job. Example: don't put invoice calculation logic and invoice printing logic in the same class; split them into `InvoiceCalculator` and `InvoicePrinter`. **OCP**: classes should be **open for extension but closed for modification** — you should add new behavior by **adding new code** (like a new derived class), not by editing existing tested code. Example: adding a new `PaypalPayment` class instead of adding `if-else` branches inside an existing `Payment` class.

---

## Question 93

**Topic:** SOLID Principles & Design Concepts

**Difficulty:** Hard

**Interview Question:** Explain the Liskov Substitution Principle (LSP) and Interface Segregation Principle (ISP) with examples.

**Answer**
**LSP**: objects of a derived class should be **replaceable** for objects of the base class **without breaking the program**. Classic violation: a `Square` extending `Rectangle` that overrides `setWidth()` to also change height — this breaks code expecting normal `Rectangle` behavior. **ISP**: clients shouldn't be forced to depend on interfaces they **don't use** — instead of one large `Machine` interface with `print()`, `scan()`, `fax()`, split it into smaller interfaces so a simple `Printer` class doesn't need to implement `fax()`.

---

## Question 94

**Topic:** SOLID Principles & Design Concepts

**Difficulty:** Hard

**Interview Question:** Explain the Dependency Inversion Principle (DIP) with an example.

**Answer**
DIP states that **high-level modules should not depend on low-level modules** — both should depend on **abstractions** (interfaces), and details should depend on those abstractions too. Example: instead of a `NotificationService` directly depending on a concrete `EmailSender` class, it should depend on an abstract `IMessageSender` interface — so you can later plug in `SMSSender` or `PushNotificationSender` without changing `NotificationService`'s code. This makes systems flexible and easy to unit-test using mocks.

---

# Topic 19: Scenario-Based Questions

*Note: Scenario questions on "why virtual destructors matter" and "the diamond problem" are already covered in-depth in Topics 9 and 7 — they're not repeated here to avoid duplication.*

## Question 95

**Topic:** Scenario-Based Questions

**Difficulty:** Hard

**Interview Question:** When would you use inheritance instead of composition, and vice versa?

**Answer**
Use **inheritance** when there's a genuine **IS-A relationship** and the derived class needs to reuse and extend base class behavior polymorphically, e.g., `Manager IS-A Employee`. Use **composition** when it's a **HAS-A relationship**, or when you want more flexibility to change behavior at runtime without a rigid class hierarchy, e.g., a `Car` HAS-A `Engine` (you could even swap engine types). The general design guideline is: **"favor composition over inheritance"** since it produces more flexible, loosely-coupled code.

---

## Question 96

**Topic:** Scenario-Based Questions

**Difficulty:** Hard

**Interview Question:** How would you design a Library Management System using OOP?

**Answer**
I'd start with core classes: `Book` (title, ISBN, status), `Member` (name, memberId, borrowed books), and `Librarian`. A `Library` class would **aggregate** `Book` and `Member` objects, and manage operations like `issueBook()` and `returnBook()`. I'd use **inheritance** for a `User` base class with `Member` and `Librarian` as derived types (different permissions), and **encapsulation** to keep book status/availability private with controlled access methods.

---

## Question 97

**Topic:** Scenario-Based Questions

**Difficulty:** Hard

**Interview Question:** Why should data members always be made private?

**Answer**
Making data members private **prevents uncontrolled or invalid modification** from outside the class — for example, stopping someone from directly setting a bank balance to a negative number. It enforces that all changes go through **validated public methods** (getters/setters), which also means the internal representation can be changed later **without breaking external code** that depends only on the public interface. This is the foundation of encapsulation and data security.

---

## Question 98

**Topic:** Scenario-Based Questions

**Difficulty:** Hard

**Interview Question:** Why is polymorphism especially useful in large-scale applications?

**Answer**
In large applications, polymorphism lets you write code against a **common base interface** and add new derived classes **without modifying existing, already-tested code** — directly supporting the Open/Closed Principle. For example, a payment processing module can call `process()` on any `PaymentMethod`, and adding a new payment type later requires **zero changes** to the existing checkout logic — reducing regression risk and easing team collaboration on large codebases.

---

## Question 99

**Topic:** Scenario-Based Questions

**Difficulty:** Hard

**Interview Question:** Explain abstraction using an ATM or car example.

**Answer**
When you use an **ATM**, you interact with a simple interface — insert card, enter PIN, select "withdraw" — while complex operations like verifying your bank balance, communicating with the bank's server, and dispensing exact currency notes happen behind the scenes, completely hidden from you. Similarly, a **car's accelerator pedal** abstracts away the entire fuel injection and combustion process — you just press the pedal. Both show abstraction: exposing a simple interface while hiding complex implementation.

---

## Question 100

**Topic:** Scenario-Based Questions

**Difficulty:** Hard

**Interview Question:** What would you do differently when composition is more suitable than inheritance in a real design?

**Answer**
If two classes don't share a true IS-A relationship, I would give the "whole" class a **member object** of the "part" class rather than inherit, e.g., a `Car` class holding an `Engine` object instead of inheriting from `Engine` (a car "is not" an engine). This avoids exposing the part's full interface unnecessarily, allows swapping implementations easily (e.g., swap a `PetrolEngine` for an `ElectricEngine`), and keeps the class hierarchy shallow and easier to maintain.

---

---

# ⭐ Topic 20: Top 30 Most Frequently Asked OOP Questions in TCS

*This is your final 10-minute revision list — the questions that come up again and again across TCS Prime, TCS Digital, and TCS Ninja interviews. Answers here are intentionally short (1–2 lines) for rapid recall. Full explanations for each are in the topic-wise sections above.*

1. **What is OOP?** — A paradigm that models programs as interacting objects, built on encapsulation, abstraction, inheritance, and polymorphism. *(Q1)*
2. **Class vs Object?** — Class is a blueprint (no memory); object is an instance (memory allocated). *(Q11)*
3. **What is encapsulation?** — Binding data and methods together while hiding internal data using access specifiers. *(Q36)*
4. **What is abstraction?** — Showing only essential features while hiding implementation complexity. *(Q40)*
5. **Encapsulation vs Abstraction?** — Encapsulation hides data (implementation-level); abstraction hides complexity (design-level). *(Q44)*
6. **What is inheritance?** — A derived class acquiring properties/behavior of a base class for reusability. *(Q45)*
7. **Types of inheritance?** — Single, Multiple, Multilevel, Hierarchical, Hybrid. *(Q46)*
8. **What is polymorphism?** — One interface, many implementations — "many forms." *(Q50)*
9. **Compile-time vs Runtime polymorphism?** — Overloading (compile-time) vs Overriding with virtual functions (runtime). *(Q50)*
10. **What is a constructor?** — Special function auto-called on object creation, same name as class, no return type. *(Q18)*
11. **What is a destructor?** — Special function auto-called on object destruction, `~ClassName()`, no parameters. *(Q24)*
12. **Constructor vs Destructor?** — Constructor initializes on creation (overloadable); destructor cleans up on destruction (not overloadable). *(Q25)*
13. **Public vs Private vs Protected?** — Public: accessible everywhere. Private: same class only. Protected: same class + derived classes. *(Q31)*
14. **What is function overloading?** — Same function name, different parameter list, resolved at compile time. *(Q59)*
15. **What is function overriding?** — Derived class redefines a base class virtual function with the same signature. *(Q64)*
16. **Overloading vs Overriding?** — Overloading = same class, different params, compile-time. Overriding = base/derived, same signature, runtime. *(Q66)*
17. **What is a virtual function?** — A base class function marked `virtual` that can be overridden and resolved via dynamic binding. *(Q55)*
18. **What is a pure virtual function?** — A virtual function with no body (`=0`), forcing derived classes to implement it; makes the class abstract. *(Q41, Q58)*
19. **Why virtual destructors?** — To ensure the derived class destructor runs when deleting via a base pointer, avoiding memory leaks. *(Q56)*
20. **What is the diamond problem?** — Ambiguity from multiple inheritance where two paths lead to the same base class; solved with virtual inheritance. *(Q48, Q49)*
21. **What is a friend function?** — A non-member function granted access to a class's private/protected members. *(Q73)*
22. **What is the `this` pointer?** — An implicit pointer inside member functions pointing to the calling object. *(Q71)*
23. **Static vs Non-static members?** — Static members are shared across all objects (one copy); non-static members get a separate copy per object. *(Q68)*
24. **Stack vs Heap?** — Stack: automatic, fast, limited size. Heap: manual (`new`/`delete`), larger, must be freed explicitly. *(Q76)*
25. **Deep copy vs Shallow copy?** — Shallow copy copies pointer addresses (shared memory); deep copy duplicates the actual memory (independent copies). *(Q79)*
26. **Association vs Aggregation vs Composition?** — Association: general relation. Aggregation: HAS-A, weak ownership. Composition: HAS-A, strong ownership (lifetimes tied). *(Q89, Q90)*
27. **IS-A vs HAS-A?** — IS-A is inheritance (specialization); HAS-A is composition/aggregation (containment). *(Q91)*
28. **static_cast vs dynamic_cast?** — static_cast: compile-time, no safety check. dynamic_cast: runtime-checked, used for safe downcasting in polymorphic hierarchies. *(Q82)*
29. **Abstract class vs Interface?** — Abstract class can mix implemented + pure virtual methods; interface has only method declarations, no implementation. *(Q43)*
30. **Why are destructors made virtual, and why keep data members private?** — Virtual destructors ensure correct cleanup during polymorphic deletion; private data members enforce controlled, validated access and protect object integrity. *(Q56, Q97)*

---

## Final Interview Tips

* Always answer OOP questions with a **short definition + one real-world/code example** — TCS interviewers value clarity over textbook depth.
* When asked a "vs" question, structure your answer as **two crisp contrasting points**, not a long essay.
* For scenario questions, briefly explain the **design reasoning** ("I'd use composition here because…") rather than just naming the concept.
* Keep your tone confident and conversational — this handbook mirrors exactly how you should speak in the interview room.

**All the best for your TCS Prime interview!**
