# What is `!!` in C

`!` is negation. So `!!` is negation of negation. What is important is the fact that the result will be an `int`.

- `!!x` if `x == 0` is `!!0`, that is `!1`, that is `0`.
- `!!x` if `x != 0` is `!!(!0)`, that is `!!1`, that is `!0`, that is `1`.

`!!` is used commonly if you want to convert any non-zero value to 1 while being certain that 0 remains a 0.

And indeed, `!!NULL == NULL`, since `!!NULL == !!0` and `!!0 == !1` and finally `!1 == 0`.

Consequently, in the short piece of code you cited the array subscript will be either `0` if the value of the expression in parenthesis is `NULL`, and `1` otherwise.