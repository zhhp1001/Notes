

Copy constructor can be called either implicitly or explicitly.

```C++
Subject *subject1 = new Subject;

// In this case it is explicitly called.
Subject *subject2 = new Subject(*subject1);

// In this case it is implicitly called.
Subject subject3 = *subject1;
```