# Function
## Pointers to Functions
- A function pointer is just that—a pointer that denotes a function
```
// pf points to a function returning bool that takes two const string references
bool (*pf)(const string &, const string &);  // uninitialized

```
- pf is preceded by a *, so pf is a pointer. 
- To the right is a parameter list, which means that pf points to a function.
- Looking left, we find that the type the function returns is bool. 
- Thus, pf points to a function that has two const string& parameters and returns bool.
