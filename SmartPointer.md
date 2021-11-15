### Smart Pointers

- In C++, dynamic memory is managed through a pair of operators: new, which
allocates, and optionally initializes, an object in dynamic memory and returns a pointer
to that object;

- delete, which takes a pointer to a dynamic object, destroys that
object, and frees the associated memory.

-Dynamic memory is problematic because it is surprisingly hard to ensure that we
free memory at the right time.

- Case 1:
- Either we forget to free the memory—in which case we have a memory leak
- Case2:
- Free the memory when there are still pointers referring to
that memory—in which case we have a pointer that refers to memory that is no
longer valid.

The shared_ptr Class

Smart pointers are templates, therefore, when we create
a smart pointer, we must supply additional information—in this case, the type to which
the pointer can point.

```
shared_ptr<string> p1;    // shared_ptr that can point at a string
shared_ptr<list<int>> p2; // shared_ptr that can point at a list of ints

```

### The make_shared Function

The safest way to allocate and use dynamic memory is to call a library function named
make_shared.

This function allocates and initializes an object in dynamic memory
and returns a shared_ptr that points to that object.

```
// shared_ptr that points to an int with value 42
shared_ptr<int> p3 = make_shared<int>(42);
// p4 points to a string with value 9999999999
shared_ptr<string> p4 = make_shared<string>(10, '9');

```


### Copying and Assigning shared_ptrs

Shared_ptr has an associated counter, usually referred to
as a reference count. Whenever we copy a shared_ptr, the count is incremented.
the counter associated with a shared_ptr is incremented
1) when we use it to initialize another shared_ptr, 
2) when we use it as the right-hand operand of an
assignment,
3) when we pass it to/return it from a function by
value 

The counter is decremented 
1) when we assign a new value to
the shared_ptr
2) when the shared_ptr itself is destroyed, such as when a local shared_ptr goes out of scope

Once a shared_ptr’s counter goes to zero, the shared_ptr automatically frees
the object that it manages

shared_ptr s Automatically Destroy Their Objects …

The destructor for shared_ptr decrements the reference count of the object to
which that shared_ptr points. If the count goes to zero, the shared_ptr
destructor destroys the object to which the shared_ptr points and frees the memory
used by that object.


### ..and Automatically Free the Associated Memory


 ### Managing Memory Directly

new operator allocates memory, and delete frees memory allocated by new.

Using new to Dynamically Allocate and Initialize Objects

Objects allocated on the free store are unnamed, so new offers no way to name the
objects that it allocates. Instead, new returns a pointer to the object it allocates

```
int *pi = new int;      // pi points to a dynamically allocated,
                        // unnamed, uninitialized int
```

This new expression constructs an object of type int on the free store and returns a
pointer to that object.



We can initialize a dynamically allocated object using direct initialization.We can use traditional construction (using parentheses), and under the new
standard, we can also use list initialization (with curly braces).

```
int *pi = new int(1024); // object to which pi points has value 1024
string *ps = new string(10, '9');   // *ps is "9999999999"
// vector with ten elements with values from 0 to 9
vector<int> *pv = new vector<int>{0,1,2,3,4,5,6,7,8,9};
```

### Dynamically Allocated const Objects

It is legal to use new to allocate const objects
Like any other const, a dynamically allocated const object must be initialized.

```
// allocate and initialize a const int
const int *pci = new const int(1024);
// allocate a default-initialized const empty string
const string *pcs = new const string;

```
### Memory Exhaustion
Once a program has used all of its available memory, new expressions will fail
If new is unable to allocate the requested storage, it throws an exception of type bad_alloc

```
// if allocation fails, new returns a null pointer
int *p1 = new int; // if allocation fails, new throws std::bad_alloc
int *p2 = new (nothrow) int; // if allocation fails, new returns a null
pointer

```

## Freeing Dynamic Memory

We return memory through a delete expression. 
A delete expression takes a pointer to the object we want to free

Like new, a delete expression performs two actions: It destroys the object to which
its given pointer points, and it frees the corresponding memory.







### Pointer Values and delete

Deleting a pointer to memory that was not allocated
by new, or deleting the same pointer value more than once, is undefined

```
int i,
double
delete
delete
delete
delete
delete
*pi1 = &i, *pi2 = nullptr;
*pd = new double(33), *pd2 = pd;
i;   // error: i is not a pointer
pi1; // undefined: pi1 refers to a local
pd;  // ok
pd2; // undefined: the memory pointed to by pd2 was already freed
pi2; // ok: it is always ok to delete a null pointer
```
The compiler will generate an error for the delete of i because it knows that i is
not a pointer. The errors associated with executing delete on pi1 and pd2 are
more insidious: In general, compilers cannot tell whether a pointer points to a
statically or dynamically allocated object. Similarly, the compiler cannot tell whether
memory addressed by a pointer has already been freed. Most compilers will accept
these delete expressions, even though they are in error.


## Dynamically Allocated Objects Exist until They Are Freed


### Resetting the Value of a Pointer after a delete …

When we delete a pointer, that pointer becomes invalid. Although the pointer is
invalid, on many machines the pointer continues to hold the address of the (freed)
dynamic memory.

After the delete, the pointer becomes what is referred to as a
dangling pointer. A dangling pointer is one that refers to memory that once held an
object but no longer does so.


### ...Provides Only Limited Protection

```
int *p(new int(42));  // p points to dynamic memory
auto q = p;           // p and q point to the same memory
delete p;    // invalidates both p and q
p = nullptr; // indicates that p is no longer bound to an object

```
Here both p and q point at the same dynamically allocated object. We delete that
memory and set p to nullptr, indicating that the pointer no longer points to an
object. However, resetting p has no effect on q, which became invalid when we
deleted the memory to which p (and q!) pointed. In real systems, finding all the
pointers that point to the same memory is surprisingly difficult


### Don’t Mix Ordinary Pointers and Smart Pointers …

A shared_ptr can coordinate destruction only with other shared_ptrs that are
copies of itself. Indeed, this fact is one of the reasons we recommend using
make_shared rather than new. That way, we bind a shared_ptr to the object at
the same time that we allocate it. There is no way to inadvertently bind the same
memory to more than one independently created shared_ptr

### Smart Pointers and Exceptions

we noted that programs that use exception handling to continue
processing after an exception occurs need to ensure that resources are properly freed
if an exception occurs. One easy way to make sure resources are freed is to use smart
pointers.

```
void f()
{
    shared_ptr<int> sp(new int(42)); // allocate a new object
   // code that throws an exception that is not caught inside f
} // shared_ptr freed automatically when the function ends
```

When a function is exited, whether through normal processing or due to an exception,
all the local objects are destroyed. In this case, sp is a shared_ptr, so destroying
sp checks its reference count. Here, sp is the only pointer to the memory it manages;
that memory will be freed as part of destroying sp.
In contrast, memory that we manage directly is not automatically freed when an
exception occurs. If we use built-in pointers to manage memory and an exception
occurs after a new but before the corresponding delete, then that memory won’t be
freed



```
void f()
{
    int *ip = new int(42);     // dynamically allocate a new object
    // code that throws an exception that is not caught inside f
    delete ip;                 // free the memory before exiting
}
```
If an exception happens between the new and the delete, and is not caught inside
f, then this memory can never be freed. There is no pointer to this memory outside
the function f. Thus, there is no way to free this memory.


### unique_ptr
A unique_ptr “owns” the object to which it points.
only one
unique_ptr at a time can point to a given object. The object to which a
unique_ptr points is destroyed when the unique_ptr is destroyed.

```
unique_ptr<double> p1;  // unique_ptr that can point at a double
unique_ptr<int> p2(new int(42)); // p2 points to int with value 42

```
Because a unique_ptr owns the object to which it points, unique_ptr does not
support ordinary copy or assignment
```
unique_ptr<string> p1(new string("Stegosaurus"));
unique_ptr<string> p2(p1);  // error: no copy for unique_ptr
unique_ptr<string> p3;
p3 = p2;                    // error: no assign for unique_ptr

```

Although we can’t copy or assign a unique_ptr, we can transfer ownership from one
(nonconst) unique_ptr to another by calling release or reset.

The release member returns the pointer currently stored in the unique_ptr and
makes that unique_ptr null.

The reset member takes an optional pointer and repositions the unique_ptr to
point to the given pointer. If the unique_ptr is not null, then the object to which
the unique_ptr had pointed is deleted.






### weak_ptr

weak_ptr points to an object that is managed by
a shared_ptr. Binding a weak_ptr to a shared_ptr does not change the
reference count of that shared_ptr. Once the last shared_ptr pointing to the
object goes away, the object itself will be deleted. That object will be deleted even if
there are weak_ptrs pointing to it.
Because the object might no longer exist, we cannot use a weak_ptr to access its
object directly. To access that object, we must call lock. The lock function checks
whether the object to which the weak_ptr points still exists. If so, lock returns a
shared_ptr to the shared object.


## Dynamic Arrays

### new and Arrays

new to allocate an array of objects by specifying the number of objects to allocate in a pair of square brackets after a type name.

new allocates the requested number of objects and (assuming the allocation succeeds) returns a pointer
to the first one
```
int *pia = new int[get_size()];

```

### Allocating an Array Yields a Pointer to the Element Type

When we use new to allocate an array, we do not get an object with an array type. Instead, we get a pointer to the element type of the array.

Because the allocated memory does not have an array type, we cannot call begin
or end  on a dynamic array. These functions use the array dimension
(which is part of an array’s type) to return pointers to the first and one past the last
elements, respectively. For the same reasons, we also cannot use a range for to
process the elements in a (so-called) dynamic array.

### Initializing an Array of Dynamically Allocated Objects

```
// block of ten ints each initialized from the corresponding initializer
int *pia3 = new int[10]{0,1,2,3,4,5,6,7,8,9};
// block of ten strings; the first four are initialized from the given initializers
// remaining elements are value initialized

string *psa3=new string[10]{"a","an","the",string(3,'x')};

```
As when we list initialize an object of built-in array type, the
initializers are used to initialize the first elements in the array. If there are fewer
initializers than elements, the remaining elements are value initialized. If there are
more initializers than the given size, then the new expression fails and no storage is
allocated. In this case, new throws an exception of type bad_array_new_length.

It Is Legal to Dynamically Allocate an Empty Array

Calling new[n] with n equal to 0 is legal even though we
cannot create an array variable of size 0.

### Freeing Dynamic Arrays

To free a dynamic array, we use a special form of delete that includes an empty pair
of square brackets
```
delete p;     // p must point to a dynamically allocated object or be null
delete [] pa; // pa must point to a dynamically allocated array or be null

```
The second statement destroys the elements in the array to which pa points and frees
the corresponding memory. Elements in an array are destroyed in reverse order. That
is, the last element is destroyed first, then the second to last, and so on.
When we delete a pointer to an array, the empty bracket pair is essential: It
indicates to the compiler that the pointer addresses the first element of an array of
objects. If we omit the brackets when we delete a pointer to an array (or provide
them when we delete a pointer to an object), the behavior is undefined.

## Smart Pointers and Dynamic Arrays

### Unique pointer to dynamically allocated Array

The library provides a version of unique_ptr that can manage arrays allocated by
new. To use a unique_ptr to manage a dynamic array, we must include a pair of
empty brackets after the object type.

```
//up points to an array of ten uninitialized ints
unique_ptr<int[]> up(new int[10]);
up.release();   // automatically uses delete[] to destroy its pointer

```
The brackets in the type specifier (<int[]>) say that up points not to an int but to
an array of ints. Because up points to an array, when up destroys the pointer it
manages, it will automatically use delete[]
When a unique_ptr points to an array, we cannot use the dot and arrow member
access operators. After all, the unqiue_ptr points to an array, not an object so these
operators would be meaningless. On the other hand, when a unqiue_ptr points to
an array, we can use the subscript operator to access the elements in the array.


