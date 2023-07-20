# switch - crosses initialization error

The C++ standard says:

> It is possible to transfer into a block, but not in a way that bypasses declarations with initialization. A program that jumps from a point where a local variable with automatic storage duration is not in scope to a point where it is in scope is ill-formed unless the variable has POD type (3.9) and is declared without an initializer.

The cases in `switch` are considered as a "jump".

Just put all objects and variables initializations before your switch, and everything will be fine.

Consider this code:

```cpp
switch(k)
{
    case 1:
        int t = 4;
    break;
    default:
    break;
}
```

It will cause a "crosses initialization" error, because it is possible to skip the initialization of t, but after that it will still *be in scope*, even though it was never created in the first place.

Now consider this:

```cpp
switch(k)
{
    case 1:
    {
        int t = 4;
    }
    break;
    default:
    break;
}
```

Here, you will *not* have the error, because the variable is inside a block, and will die at the end of the block ( at the closing `{` ), so after that it will *not* be in scope in any case.

To fix the first case, you just need to do:

```cpp
int t = 0;
switch(k)
{
    case 1:
        t = 4;
    break;
    default:
    break;
}
```