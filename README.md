# Robotics_And_OOP
This repository has project for displaying c++ and OOP concepts and utilizing it for path planning
## C++ and OOP concepts 
In this project we have used the following concepts of c++ and OOP:
### OOP 
It is a style of programming. It has the following four features:
1) Inheritance
2) Abstraction
3) Encapsulation
4) Polymorphism
### Class
- A class in C++ is the building block, that leads to Object-Oriented programming.
- Fundamental idea behind **Class** are **data abstraction** and **encapsulation**.
**Data abstraction** is a programming technique that relies on **interface** and **implementation**. The interface of a class has operation the user of the class can execute.Implementation has class data members,and function implementation of the operation defined in interface.

- It is a user-defined data type, which holds its own data members and member functions, which can be accessed and used by creating an instance of that class. 
- A C++ class is like a blueprint for an object.
- When a class is defined, only the specification for the object is defined; no memory or storage is allocated. To use the data and access functions defined in the class, you need to create objects.
- In C++, a structure is the same as a class except for a few differences. 
- The most important of them is security. A Structure is not secure and cannot hide its implementation details from the end-user while a class is secure and can hide its programming and designing details.

Following are the points that expound on this difference:
  1) Members of a class are private by default and members of a structure are public by default. 

### Additional Features of Class

**We can overload member function of a class**

**Defining a Type Member**

```
class Screen {
public:
    typedef std::string::size_type pos;
private:
    pos cursor = 0;
    pos height = 0, width = 0;
    std::string contents;
};

```
**Inline Function**

**Aggregate Classes**
- An aggregate class gives users direct access to its members and has special
initialization syntax. 
- A class is an aggregate if:\
      - All of its data members are public\
      - It does not define any constructors\
      - It has no in-class initializers\
      - It has no base classes or virtual functions\

- The initializers must appear in declaration order of the data members. That is, the
initializer for the first member is first, for the second is next, and so on.

```
struct Data {
    int ival;
    string s;
};

```
They are not used much as they have the following drawbacks:
- It requires that all the data members of the class be public.
- It puts the burden on the user of the class (rather than on the class author) to
correctly initialize every member of every object. Such initialization is tedious and
error-prone because it is easy to forget an initializer or to supply an
inappropriate initializer.
- Modification is hard.

### Objects
An Object is an instance of a Class.

### Abstract Class
A class that has atleast one pure virtual function, is an Abstract Class. 
Generally, abstract class is used as the base class in inhertance, a class derived form abstract class must define pure virtual function else it would also be a abstract class and we cannot create objects out of it.
Abstract classes can't be used for:
- Variables or member data
- Argument types
- Function return types
- Types of explicit conversions

### Access Specifiers

Access modifiers are used to implement an important aspect of Object-Oriented Programming known as Data Hiding. 
1) Public - members are accessible from outside the class
2) Private - members cannot be accessed (or viewed) from outside the class
3) Protected - members cannot be accessed from outside the class, however, they can be accessed in inherited classes.

- A class may contain zero or more access specifiers, and there are no restrictions on
how often an access specifier may appear. 

- Each access specifier specifies the access
level of the succeeding members. The specified access level remains in effect until the
next access specifier or the end of the class body.

### Constructors 

- Constructors are special class members which are called by the compiler every time an object of that class is instantiated. 
- Constructors have the same name as the class and may be defined inside or outside the class definition.
- Constructors have no return type, they only have a function body and parameter.
- **Constructor cannot be declared** **Const**
- If we donot have a constructor for our class then **default constructor** is called.
- We use **=default** explicity with default constructor to tell the complier that the constructor in consideration is default constructor.

#### Constructor Initialization List

- It specifies initial values for one or more data members of the
object being created. 
- The constructor initializer is a list of member names, each of
which is followed by that member???s initial value in parentheses (or inside curly
braces). Multiple member initializations are separated by commas.
```
Sales_data(const std::string &s):
           bookNo(s), units_sold(0), revenue(0){ }
     
```
- Members are initialized in the order in which they appear in the class definition: The
first member is initialized first, then the next, and so on.
- The order in which initializers appear in the constructor initializer list does not change the order of initialization.
- The order of initialization often doesn???t matter. However, if one member is initialized in terms of another, then the order in which members are initialized is crucially important.

There are 3 types of constructors:
  1) Default constructors/synthesized default constructor.
  2) Parameterized constructors
  3) Copy constructors
  4) Delegating constructors

#### Default constructor

- The compiler generates a default constructor automatically only if a class declares no constructors this constructor is called **synthesized default constructor**

```
Sales_data() = default;
```

- The =default can appear with the declaration inside the class body or on the definition
outside the class body.

- Like any other function, if the = default appears inside the
class body, the default constructor will be inlined; if it appears on the definition
outside the class, the member will not be inlined by default.

- We must not depend on synthesized default constructor as it might give wrong innitialzations in some cases and can lead to a unknown behaviors.

**Reason 1**

Some classes, the synthesized default constructor does the wrong thing. 
Objects of built-in or compound type (such as arrays and pointers) that are defined inside a block
have undefined value when they are default initialized. The same rule
applies to members of built-in type that are default initialized. Therefore, classes that
have members of built-in or compound type should ordinarily either initialize those
members inside the class or define their own version of the default constructor.

**Reason 2**

Sometimes the compiler is unable to synthesize one. For example, if a class has a
member that has a class type, and that class doesn???t have a default constructor, then
the compiler can???t initialize that member. For such classes, we must define our own
version of the default constructor. Otherwise, the class will not have a usable default
constructor.

#### Parameterized constructor

#### Copy constructor

#### Delegating constructors

- A delegating constructor uses another constructor from its own class to perform its initialization. It is said to ???delegate??? some (or all) of its work
to this other constructor.

- Like any other constructor, a delegating constructor has a member initializer list and a function body. 
- In a delegating constructor, the member initializer list has a single entry that is the name of the class itself. Like other member initializers, the name of
the class is followed by a parenthesized list of arguments. The argument list must match another constructor in the class.
- When a constructor delegates to another constructor, the constructor initializer list
and function body of the delegated-to constructor are both executed.

```
class class_a {
public:
    class_a() {}
    // member initialization here, no delegate
    class_a(string str) : m_string{ str } {}

    //can???t do member initialization here
    // error C3511: a call to a delegating constructor shall be the only member-initializer
    class_a(string str, double dbl) : class_a(str) , m_double{ dbl } {}

    // only member assignment
    class_a(string str, double dbl) : class_a(str) { m_double = dbl; }
    double m_double{ 1.0 };
    string m_string;
};

```

### Friend
- A class can allow another class or function to access its nonpublic members by making that class or function a friend.
- Friends are not members of the class and are not affected by the access control of the section in which they are declared.
- We group friend function and class at the start for better readability.
```
class Sales_data {
// friend declarations for nonmember Sales_data operations added
friend Sales_data add(const Sales_data&, const Sales_data&);
friend std::istream &read(std::istream&, Sales_data&);
friend std::ostream &print(std::ostream&, const Sales_data&);
// other members and access specifiers as before
public:
    Sales_data() = default;
    Sales_data(const std::string &s, unsigned n, double p):
               bookNo(s), units_sold(n), revenue(p*n) { }
    Sales_data(const std::string &s): bookNo(s) { }
    Sales_data(std::istream&);
    std::string isbn() const { return bookNo; }
    Sales_data &combine(const Sales_data&);
private:
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};
// declarations for nonmember parts of the Sales_data interface
Sales_data add(const Sales_data&, const Sales_data&);
std::istream &read(std::istream&, Sales_data&);
std::ostream &print(std::ostream&, const Sales_data&);

```
- **Although overloaded functions share a common name, they are still different
functions. Therefore, a class must declare as a friend each function in a set of
overloaded functions that it wishes to make a friend**

### Destructor

Destructor is an instance member function which is invoked automatically whenever an object is going to be destroyed. Meaning, a destructor is the last function that is going to be called before an object is destroyed.
- A destructor function is called automatically when the object goes out of scope: 
1) The function ends 
2) The program ends 
3) A block containing local variables ends 
4) A delete operator is called  
- There can only one destructor in a class with classname preceded by ~, no parameters and no return type.
- It is possible to have pure virtual destructor. Pure virtual destructors are legal in standard C++ and one of the most important things to remember is that if a class contains a pure virtual destructor, it must provide a function body for the pure virtual destructor. You may be wondering why a pure virtual function requires a function body. The reason is because destructors (unlike other functions) are not actually ???overridden???, rather they are always called in the reverse order of the class derivation. This means that a derived class??? destructor will be invoked first, then base class destructor will be called. If the definition of the pure virtual destructor is not provided, then what function body will be called during object destruction? Therefore the compiler and linker enforce the existence of a function body for pure virtual destructors
- Cannot be declared as const, volatile, or static. However, they can be invoked for the destruction of objects declared as const, volatile, or static.

### Setters and Getter Methods

The meaning of Encapsulation, is to make sure that "sensitive" data is hidden from users. To achieve this, you must declare class variables/attributes as private (cannot be accessed from outside the class). If you want others to read or modify the value of a private member, you can provide public get and set methods.

### Inheritance   

The capability of a class to derive properties and characteristics from another class is called Inheritance. Inheritance is one of the most important feature of Object Oriented Programming.
- This reduces the chances of error and data redundancy and increases code resuablility.
- A derived class can access public class member and public attributes of the class but not private and protected attributes/member function.
- Modes of Inheritance
   1) Public mode: If we derive a sub class from a public base class. Then the public member of the base class will become public in the derived class and protected members of the base class will become protected in derived class.
    2) Protected mode: If we derive a sub class from a Protected base class. Then both public member and protected members of the base class will become protected in derived class.
    3) Private mode: If we derive a sub class from a Private base class. Then both public member and protected members of the base class will become Private in derived class. 

![Screenshot from 2021-11-09 09-35-46](https://user-images.githubusercontent.com/93336207/140943856-c2f42cac-bd81-4f51-9d73-ddfaecef28bc.png)

Type of inheritance:
1) Multiple Inheritance: Multiple Inheritance is a feature of C++ where a class can inherit from more than one classes. i.e one sub class is inherited from more than one base classes.
2) Single Inheritance: In single inheritance, a class is allowed to inherit from only one class. i.e. one sub class is inherited by one base class only.
3) Hierarchical Inheritance: In this type of inheritance, more than one sub class is inherited from a single base class. i.e. more than one derived class is created from a single base class.

- Friend class can access class protected and private memeber function and attributes. We must make a proper decision while making a class friend as it leads to  
losse binding.
- Friendship is not inherited by child classes.

### Virtual Functions 

A function that only has declaration and may or may not have a defination in the base class, is called a Virtual function. 
If a class has a virtual function it doesnot becomes an Abstract class, for it to be abstract class it has to have a pure virtual function.
When we have a virtual function in our base class, we can change the defination for it in our derived class by overriding the function.
- Virtual functions cannot be static.
- A virtual function can be a friend function of another class.
- Virtual functions should be accessed using pointer or reference of base class type to achieve run time polymorphism.
- The prototype of virtual functions should be the same in the base as well as derived class.
- A class may have virtual destructor but it cannot have a virtual constructor. (virtual destructor are found of most use in abstract class)
- They help implement runtime polymorphism.
- Working of virtual functions
  1) If object of that class is created then a virtual pointer(VPTR) is inserted as a data member of the class to point to VTABLE of that class. For each new object created, a new virtual pointer is inserted as a data member of that class.
  2) Irrespective of object is created or not, a static array of function pointer called VTABLE where each cell contains the address of each virtual function contained in that class.
### Pure Virtual Function

### Function Overloading 

Function overloading, multiple functions can have the same name with different parameters.

### Smart Pointers


## Code Documentation 
Doxygen is a code documneting tool.A C or C++ style comment block with some additional markings is done so that doxygen knows it is a piece of structured text that needs to end up in the generated documentation. The next section presents the various styles supported by doxygen. 

# Extra Concepts And Important points
## Concepts
### Operator Overloading
The operator keyword declares a function specifying what operator-symbol means when applied to instances of a class. This gives the operator more than one meaning, or "overloads" it. The compiler distinguishes between the different meanings of an operator by examining the types of its operands.
The name of an overloaded operator is operator x, where x is the operator.
- You cannot define new operators while doing operator overloading.
- You cannot redefine the meaning of operators when applied to built-in data types.
- All overloaded operators except assignment (operator=) are inherited by derived classes.

### Late and Early Binding

### Templates 

### Constant Member Function 

- The const member functions are the functions which are declared as constant in the program.
- **The object called by these functions cannot be modified**.
- It is recommended to use **const** keyword so that accidental changes to object are avoided.
- A const member function can be called by any type of object.
- Non-const functions can be called by non-const objects only.
- The **const** keyword is required in both the declaration and the definition.
```
// constant_member_function.cpp
class Date
{
public:
   Date( int mn, int dy, int yr );
   int getMonth() const;     // A read-only function
   void setMonth( int mn );   // A write function; can't be const
private:
   int month;
};

int Date::getMonth() const
{
   return month;        // Doesn't modify anything
}
void Date::setMonth( int mn )
{
   month = mn;          // Modifies data member
}
int main()
{
   Date MyDate( 7, 4, 1998 );
   const Date BirthDate( 1, 18, 1953 );
   MyDate.setMonth( 4 );    // Okay
   BirthDate.getMonth();    // Okay
   BirthDate.setMonth( 4 ); // C2662 Error
}
```

### Mutable Data member

Sometimes there is requirement to modify one or more data members of class / struct through const function even though you don???t want the function to update other members of class / struct. This task can be easily performed by using mutable keyword.

```
#include <iostream>
using std::cout;
 
class Test {
public:
  int x;
  mutable int y;
  Test() { x = 4; y = 10; }
};
int main()
{
    const Test t1;
    t1.x = 8;
    t1.y=12;
    cout << t1.x;
    cout<<t1.y;
    return 0;
}
```

```
#include <bits/stdc++.h>
#include <string.h>
using namespace std;
 
// Customer Class
class Customer {
    
    // class Variables
    string name;
    mutable string placedorder;
    int tableno;
    mutable int bill;
 
    // member methods
public:
   
    
    // constructor
    Customer(string s, string m, int a, int p)
    {
        name= s;
        placedorder=m;
        tableno = a;
        bill = p;
    }
     
    // to change the place holder
    void changePlacedOrder(string p) const
    {
        placedorder=p;
    }
   
    // change the bill
    void changeBill(int s) const { bill = s; }
   
    // to display
    void display() const
    {
        cout << "Customer name is: " << name << endl;
        cout << "Food ordered by customer is: "
             << placedorder << endl;
        cout << "table no is: " << tableno << endl;
        cout << "Total payable amount: " << bill << endl;
    }
};
 
// Driver code
int main()
{
    const Customer c1("aalap", "Ice Cream", 3, 100);
    c1.display();
    c1.changePlacedOrder("GulabJammuns");
    c1.changeBill(150);
    c1.display();
    return 0;
}
```

### Static Class Member

- Static members can be public or private.
- The type of a static data member can be const, reference, array, class type, etc.
- There is always only one copy static data member, that is shared by all the objects of the class 
- All static data is initialized to 0 when first object is created, if no other initialization is present
- They are not initialized by the class??? constructors. Moreover, in general, we may not initialize a static member inside the class. Instead, we must define and initialize each static data member outside the class body.
- They continue to exist until the program completes

### Static Member Function 

- Static member function inside or outside of the class body. 
- When we define a static member outside the class, we do not repeat the static keyword. 
- The keyword appears only with the declaration inside the class body.
- They continue to exist until the program completes
- A static member function can only acesss static data member, it would give error if we use non static member or function in them.
- They have class level scope, and donot have acess to **this** pointer of the class

## Important Points

- Member functions may be defined inside the class itself or outside the class body. Nonmember functions that are part of the interface are declared and defined outside the class.
- Functions defined in the class are **implicitly inline**
- **this:** Member functions access the object on which they were called through an extra, implicit parameter named this. When we call a member function, this is initialized with the address of the object on which the function was invoked.
- It is illegal to define a parameter or variable named **this**.
- 
