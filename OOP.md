## Inheritance
- Classes related by inheritance form a hierarchy.
- **Base class** is at the root of the hierarchy, from which the other classes inherit, directly or indirectly.
- These inheriting classes are known as derived classes. The base class defines those members that are common to the types in the hierarchy.
- Each derived class defines those members that are specific to the derived class itself.
- A derived class must specify the class(es) from which it intends to inherit. It does so in a class derivation list, which is a colon followed by a comma-separated list of base classes each of which may have an optional access specifier.
- ```
- class Bulk_quote : public Quote { // Bulk_quote inherits from Quote
public:
    double net_price(std::size_t) const override;
};
 `
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

