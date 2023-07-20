# &array and array

https://www.geeksforgeeks.org/whats-difference-between-array-and-array-for-int-array5/



any *array name itself* is a *pointer to the first element* but *& (i.e. address-of) for the array name* is a *pointer to the whole array* itself.



```c
void *p = array;   //array name, gives address of the  first element.
```

and

```c
void *q = &array;  //adress-of-array name, also gives address of the first element
                   // actually &array is of type int (*)[16] which is decayed to int * 
                   // and casted to void * here
```