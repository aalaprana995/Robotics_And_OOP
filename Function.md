# Function
## Pointers to Functions
- A function pointer is just that—a pointer that denotes a function
```
// compares lengths of two strings
bool lengthCompare(const string &, const string &);

// pf points to a function returning bool that takes two const string references
bool (*pf)(const string &, const string &);  // uninitialized

pf = lengthCompare;// pf now points to the function named lengthCompare
pf = &lengthCompare; // equivalent assignment: address-of operator is optional
```
- pf is preceded by a *, so pf is a pointer. 
- To the right is a parameter list, which means that pf points to a function.
- Looking left, we find that the type the function returns is bool. 
- Thus, pf points to a function that has two const string& parameters and returns bool.
- When we use an overloaded function, the context must make it clear which version is being used. When we declare a pointer to an overloaded function

## Function Basics
- A function definition typically consists of a return type , a name, a list of zero or more parameters, and a body.
- The parameters are specified in a comma-separated list enclosed in parentheses. 
- The actions that the function performs are specified in a statement block, referred to as the function body.
- We execute a function through the call operator, which is a pair of parentheses "()".
- The call operator takes an expression that is a function or points to a function. Inside the parentheses is a comma-separated list of arguments.
- The arguments are used to initialize the function’s parameters. The type of a call expression is the return type of the function.
### Parameter and Argument
- The type of each argument must match the corresponding parameter in the same way that the type of any initializer must match the type of the object it initializes. 
- We must pass exactly the same number of arguments as the function has parameters.Because every call is guaranteed to pass as many arguments as the function has
parameters, parameters are always initialized.
- If we have an argument  that can be converted to the type of the parameter, compiler does that and the call becomes legal
```
// factorial of val is val * (val - 1) * (val - 2) . . . * ((val - (val - 1)) * 1)
int fact(int val)
{
    int ret = 1; // local variable to hold the result as we calculate it
    while (val > 1)
        ret *= val--;  // assign ret * val to ret and decrement val
    return ret;        // return the result
}

fact("hello");       //error: wrong argument type
fact();              //error: too few arguments
fact(42, 10, 0);     //error: too many arguments
fact(3.14);          //ok: argument is converted to int

```
