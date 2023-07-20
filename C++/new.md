


My teacher explained it like this.
Think of cinema. The actual seats are memory allocations and the ticket you get are the pointers.

```C++
int * pointer = new int;
```
This would be a cinema with one seat, and pointer would be the ticket to that seat

```C++
pointer = new int [20] 
```
This would be a cinema with 20 seats and pointer would be the ticket to the first seat. pointer[1] would be the ticket to the second seat and pointer[19] would be the ticket to the last seat.

When you do int* pointer = new int; and then access pointer[2] you're letting someone sit in the aisle, meaning undefined behaviour