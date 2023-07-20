# How to print the "%" character with printf

 [Reference](https://stackoverflow.com/questions/28044161/how-to-print-the-character-with-printf)

\ is built into the language, and `'\\'` is one character. `%` is specific to the formatted IO functions - `"%%"` is two characters. 

 It's just that \ is interpreted by the compiler at compile time, while % is interpreted by `printf` at runtime. 





[Reference](https://stackoverflow.com/questions/1860159/how-to-escape-the-percent-sign-in-cs-printf)

You can escape it by posting a double '%' like this: `%%`

Using your example:

```c
printf("hello%%");
```

Escaping '%' sign is only for printf. If you do:

```c
char a[5];
strcpy(a, "%%");
printf("This is a's value: %s\n", a);
```

It will print: `This is a's value: %%`



`\045` is **compile-time escape** that is part of the **language** and will turn into `%` when compiled. `printf` is a run-time function, so it deals with bytes of your string, not with C source code, and it has its own escape sequences that are parts of the **function**. In short, `printf` is a "language inside a language", and `printf("This is a's value: %s\n", a);` gives the same result as `printf("This is a's value: \045\0163\012", a);`

 Also, you can do this: `printf("hello%c", '%');`. However, `%%` is better because it doesn't use another argument. 