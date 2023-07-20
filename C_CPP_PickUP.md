
## Does C have references?

No, it doesn't. It has pointers, but they're not quite the same thing.

In particular, all arguments in C are passed by value, rather than pass-by-reference being available as in C++. Of course, you can sort of simulate pass-by-reference via pointers:

```C
void foo(int *x)
{
    *x = 10;
}

int y = 0;
foo(&y); // Pass the pointer by value
// The value of y is now 10
```
For more details about the differences between pointers and references, see this [SO](https://stackoverflow.com/questions/57483/what-are-the-differences-between-a-pointer-variable-and-a-reference-variable) question.

## Pointer to base

https://stackoverflow.com/questions/4937180/a-base-class-pointer-can-point-to-a-derived-class-object-why-is-the-vice-versa

Uh, because the base class is not a derived class.

When you have a valid pointer to a type, then you are saying that the object pointed to will have certain data in certain locations so that we can find it. If you have a pointer to a derived object, then you are guaranteeing that the pointed-to object contains all of Derived's data members- but when you point to a Base, then it infact doesn't have that and Bad Things Happen™.

However, Derived is guaranteed to have all of the Base data members in the same locations. That's why a pointer to Base can actually point to Derived.

## Pointer to char
```C++
char *p = "Hello"; // warning
const char *p = "Hello";
```
The strings that you enter: "Hello" is "literal", because they are defined inside the program code itself (they are not read directly from disk, user input /stdin etc.).

This means that if at any point you try to write to your colors you will be directly accessing your original input and thus editing it. This would cause some undesired run-time errors.

Declaring it as a const will make sure that you will never try to write to this pointer and such a run-time error can be avoided.

Rather than try to figure out a trick to make string literals changeable (it will be highly dependent on your platform and could change over time), just use arrays:
```C++
char foo[] = "Hello";
```
The compiler will arrange for the array to get initialized from the literal and you can modify the array.