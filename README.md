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
- It is a user-defined data type, which holds its own data members and member functions, which can be accessed and used by creating an instance of that class. 
- A C++ class is like a blueprint for an object.
- When a class is defined, only the specification for the object is defined; no memory or storage is allocated. To use the data and access functions defined in the class, you need to create objects.
- In C++, a structure is the same as a class except for a few differences. 
- The most important of them is security. A Structure is not secure and cannot hide its implementation details from the end-user while a class is secure and can hide its programming and designing details.

Following are the points that expound on this difference:
  1) Members of a class are private by default and members of a structure are public by default. 

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
### Constructors 
Constructors are special class members which are called by the compiler every time an object of that class is instantiated. Constructors have the same name as the class and may be defined inside or outside the class definition.
There are 3 types of constructors:
  1) Default constructors
  2) Parameterized constructors
  3) Copy constructors
### Destructor
Destructor is an instance member function which is invoked automatically whenever an object is going to be destroyed. Meaning, a destructor is the last function that is going to be called before an object is destroyed.
- A destructor function is called automatically when the object goes out of scope: 
1) The function ends 
2) The program ends 
3) A block containing local variables ends 
4) A delete operator is called  
- There can only one destructor in a class with classname preceded by ~, no parameters and no return type.
- It is possible to have pure virtual destructor. Pure virtual destructors are legal in standard C++ and one of the most important things to remember is that if a class contains a pure virtual destructor, it must provide a function body for the pure virtual destructor. You may be wondering why a pure virtual function requires a function body. The reason is because destructors (unlike other functions) are not actually ‘overridden’, rather they are always called in the reverse order of the class derivation. This means that a derived class’ destructor will be invoked first, then base class destructor will be called. If the definition of the pure virtual destructor is not provided, then what function body will be called during object destruction? Therefore the compiler and linker enforce the existence of a function body for pure virtual destructors
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

# Extra Concepts
### Operator Overloading
The operator keyword declares a function specifying what operator-symbol means when applied to instances of a class. This gives the operator more than one meaning, or "overloads" it. The compiler distinguishes between the different meanings of an operator by examining the types of its operands.
The name of an overloaded operator is operator x, where x is the operator.
- You cannot define new operators while doing operator overloading.
- You cannot redefine the meaning of operators when applied to built-in data types.
- All overloaded operators except assignment (operator=) are inherited by derived classes.
### Late and Early Binding

### Templates 


