# Difference between char *s and char s[]

The difference here is that

```c
char *s = "Hello world";
```

will place `"Hello world"` in the *read-only parts of the memory*, and making `s` a pointer to that makes any writing operation on this memory illegal.

While doing:

```c
char s[] = "Hello world";
```

puts the literal string in read-only memory and copies the string to newly allocated memory on the stack. Thus making

```c
s[0] = 'J';
```

legal.



![img](https://media.geeksforgeeks.org/wp-content/cdn-uploads/CommonArticleDesign18-min.png)





​      