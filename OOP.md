## Inheritance
- Classes related by inheritance form a hierarchy.
- **Base class** is at the root of the hierarchy, from which the other classes inherit, directly or indirectly.
- These inheriting classes are known as derived classes. The base class defines those members that are common to the types in the hierarchy.
- Each derived class defines those members that are specific to the derived class itself.
- A derived class must specify the class(es) from which it intends to inherit. It does so in a class **derivation list**, which is a colon followed by a comma-separated list of base classes each of which may have an optional access specifier.
 ```
 class Bulk_quote : public Quote { // Bulk_quote inherits from Quote
public:
    double net_price(std::size_t) const override;
};
```
 ### Member Functions and Inheritance

- Derived classes inherit the members of their base class.
- However, a derived class needs to be able to provide its own definition for operations,in such cases, the derived class needs to **override** the
definition it inherits from the base class, by providing its own definition.
- In C++, a base class must **distinguish the functions** it expects its **derived classes** to **override** from those that it expects its derived classes to inherit without change. The base class defines as **virtual** those functions it expects its derived classes to override.
- When we **call a virtual function** through a pointer or reference , the **call** will be **dynamically bound**. Depending on the type of the object to which the reference or pointer is bound, the version in the base class or in one of its derived classes will be executed.
 - The virtual keyword appears only on the declaration inside the class and may not be used on a function definition that appears outside the class body.
- A function that is declared as virtual in the base class is implicitly virtual in the derived classes as well.
- Member functions that are not declared as virtual are resolved at compile time, not run time.

### Access Control and Inheritance

![main-qimg-db80cfa9f812b2c114c81d22f458235a](https://user-images.githubusercontent.com/93336207/141322188-960cada0-995f-4e82-8391-f2dbcab07360.png)
![Inheritance +public,+protected,+private+Summary](https://user-images.githubusercontent.com/93336207/141322608-b665fba4-b65a-4550-b1dc-9321d187b3ec.jpg)

- Access to the members of a base class is controlled by the access specifiers in the base class itself.
- The derivation access specifier has no effect on whether members (and friends) of a
derived class may access the members of its own direct base class.
```
class Base {
public:
    void pub_mem();   // public member
protected:
    int prot_mem;     // protected member
private:
    char priv_mem;    // private member
};
struct Pub_Derv : public Base {
    // ok: derived classes can access protected members
    int f() { return prot_mem; }
    // error: private members are inaccessible to derived classes
    char g() { return priv_mem; }
};
struct Priv_Derv : private Base {
    // private derivation doesn't affect access in the derived class
    int f1() const { return prot_mem; }
};
```

- A derived class member or friend may access the protected members of the base class only through a derived object. The derived class has no special access to the protected members of base-class objects.

```
class Base {
protected:
    int prot_mem;     // protected member
};
class Sneaky : public Base  {
    friend void clobber(Sneaky&);  // can access Sneaky::prot_mem
    friend void clobber(Base&);    // can't access Base::prot_mem
    int j;                          // j is private by default
};
// ok: clobber can access the private and protected members in Sneaky objects
void clobber(Sneaky &s) { s.j = s.prot_mem = 0; }
// error: clobber can't access the protected members in Base
void clobber(Base &b) { b.prot_mem = 0; }
```
### Defining a Derived Class
- A derived class must specify from which class(es) it inherits. 
- It does so in its class derivation list, which is a colon followed by a comma-separated list of names of previously defined classes.
- Each base class name may be preceded by an optional access specifier, which is one of public, protected, or private.
- A derived class must declare each inherited member function it intends to override.
### Virtual Functions in the Derived Class
- Derived classes frequently, but not always, override the virtual functions that they inherit.
- If a derived class does not override a virtual from its base, then, like any other member, the derived class inherits the version defined in its base class.
- The new standard lets a derived class explicitly note that it intends a member function to override a virtual that it inherits. It does so by specifying override after the parameter list, or after the const or reference qualifier(s) if the member is a const.
### Derived-Class Objects and the Derived-to-Base Conversion
- Derived object contains subparts corresponding to its base class(es), we
can use an object of a derived type as if it were an object of its base type(s). In
particular, we can bind a base-class reference or pointer to the base-class part of a
derived object.
- This conversion is often referred to as the derived-to-base conversion
```
Quote item;        //  object of base type
Bulk_quote bulk;   //  object of derived type
Quote *p = &item;  //  p points to a Quote object
p = &bulk;         //  p points to the Quote part of bulk
Quote &r = bulk;   //  r bound to the Quote part of bulk
```
### Derived-Class Constructors
- Each class controls how its members are initialized.
- derived object contains members that it inherits from its base, it cannot directly initialize those members. Like any other code that creates an object of the base-class type, a derived class must use a base-class constructor to initialize its base-class part.
- The base class is initialized first, and then the members of the derived class
are initialized in the order in which they are declared in the class.
```
Bulk_quote(const std::string& book, double p, std::size_t qty, double disc) :Quote(book, p), min_qty(qty), discount(disc) { }

```
### Inheritance and static Members
If a base class defines a static member (??7.6, p. 300), there is only one such
member defined for the entire hierarchy. Regardless of the number of classes derived
from a base class, there exists a single instance of each static member.
### Preventing Inheritance
- Sometimes we define a class that we don???t want others to inherit from.
- Or we might define a class for which we don???t want to think about whether it is appropriate as a
base class.
- Under the new standard, we can prevent a class from being used as a base by following the class name with **final**.
```
class NoDerived final { /*  */ }; // NoDerived can't be a base class
```
### Conversions and Inheritance
We can bind a pointer or reference to a base-class type to an object of a type derived from that base class.
### Static Type and Dynamic Type

### There Is No Implicit Conversion from Base to Derived ...

## Virtual Functions
- Ordinarily, if we do not use a function, we don???t need to supply a definition for that function. 
- However, we must define every virtual function, regardless of whether it is used, because the compiler has no way to determine whether a virtual function is used.
### Calls to Virtual Functions May Be Resolved at Run Time
When a virtual function is called through a reference or pointer, the compiler
generates code to decide at run time which function to call. The function that is called
is the one that corresponds to the dynamic type of the object bound to that pointer or
reference.
```
Quote base("0-201-82470-1", 50);
print_total(cout, base, 10);    // calls Quote::net_price
Bulk_quote derived("0-201-82470-1", 50, 5, .19);
print_total(cout, derived, 10); // calls Bulk_quote::net_price
```

**Virtuals are resolved at run time only if the call is made through a
reference or pointer. Only in these cases is it possible for an object???s
dynamic type to differ from its static type.**

### Virtual Functions in a Derived Class

- When a derived class overrides a virtual function, it may, but is not required to, repeat the virtual keyword. Once a function is declared as virtual, it remains virtual in all the derived classes
- A derived-class function that overrides an inherited virtual function must have exactly the same parameter type(s) as the base-class function that it overrides
- With one exception, the return type of a virtual in the derived class also must match the return type of the function from the base class.

```
struct B {
    virtual void f1(int) const;
    virtual void f2();
    void f3();
};
struct D1 : B {
    void f1(int) const override; // ok: f1 matches f1 in the base
    void f2(int) override; // error: B has no f2(int) function
    void f3() override;    // error: f3 not virtual
    void f4() override;    // error: B doesn't have a function named f4
 
 ```
 **Final**
 
If we want the derived class not to override the base class method we make that base class method as **final**.We can also designate a function as final. Any attempt to override a function that has been defined as final will be flagged as an error.
```
struct B {
    virtual void f1(int) const;
    virtual void f2();
    void f3();
};
struct D1 : B {
    void f1(int) const override; // ok: f1 matches f1 in the base
    void f2(int) override; // error: B has no f2(int) function
    void f3() override;    // error: f3 not virtual
    void f4() override;    // error: B doesn't have a function named f4
};
struct D2 : B {
    // inherits f2() and f3() from B and overrides f1(int)
    void f1(int) const final; // subsequent classes can't override f1
(int)
};
struct D3 : D2 {
    void f2();          // ok: overrides f2 inherited from the indirect base,
B
    void f1(int) const; // error: D2 declared f2 as final
};
```

### Virtual Functions and Default Arguments

### Preventing Virtual Mechanism
In some cases, we want to prevent dynamic binding of a call to a virtual function; we
want to force the call to use a particular version of that virtual. We can use the scope
operator to do so
```
//  calls the version from the base class regardless of the dynamic type of baseP
double undiscounted = baseP->Quote::net_price(42);
```
## Abstract Base Classes
- A class that has atleast 1 pure virtua function is called Abstract class
### Pure Virtual Function
- Unlike ordinary virtuals, a pure virtual function does not have to be defined. 
- We specify that a virtual function is a pure virtual by writing = 0 in place of a function body (i.e., just before the semicolon that ends the declaration). 
- The = 0 may appear only on the declaration of a virtual function in the class body.
- Although we cannot define objects of this type directly, constructors in classes derived would require a base class constructor when it tries to form an object of derived class.
- It is worth noting that we can provide a definition for a pure virtual. However, the
function body must be defined outside the class. That is, we cannot provide a function
body inside the class for a function that is = 0.
**A Derived Class Constructor Initializes Its Direct Base Class Only**

### Default Inheritance Protection Levels

By default, a derived class defined with the class keyword has private inheritance; a derived class defined with struct has public inheritance
```
class Base { /* ...   */ };
struct D1 : Base { /* ...   */ };   // public inheritance by default
class D2 : Base { /* ...   */ };    // private inheritance by default
```
