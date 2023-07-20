void
The void data type was introduced to make C syntactically consistent. The main reason for void is to declare functions that have no return value. The word "void" is therefore used in the sense of "empty" rather than that of "invalid".

C functions are considered by the compiler to return type int unless otherwise specified. Although the data returned by a function can legally be ignored by the function calling it, the void data type was introduced by the ANSI standard so that C compilers can issue warnings when an integer value is not returned by a function that is supposed to return one. If you want to write a function that does not return a value, simply declare it void. A function declared void has no return value and simply returns with the command return;.

Variables can be declared void as well as functions:

void my_variable;
void *my_pointer;
A variable that is itself declared void (such as my_variable above) is useless; it cannot be assigned a value, cannot be cast to another type, in fact, cannot be used in any way.

Void pointers (type void *) are a different case, however. A void pointer is a generic pointer; any pointer can be cast to a void pointer and back **without any loss of information**. Any type of pointer can be assigned to (or compared with) a void pointer, without casting the pointer explicitly.

Finally, a function call can be cast to void in order to **explicitly discard a return value**. For example, printf returns a value, but it is seldom used. Nevertheless, the two lines of code that follow are equivalent:

printf ("Hullo!\n");
(void) printf ("Hullo!\n");
There is no good reason to prefer the second line to the first, however, so using the more concise form is preferred.