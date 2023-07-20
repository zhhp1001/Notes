### What is atoi ntoa aton?

The function `inet_ntoa()` converts a network address in a struct `in_addr` to a dots-and-numbers format string.

The `n` in `ntoa` stands for network, and the `a` stands for `ASCII` for historical reasons(so it's `Network to ASCII` -- the `toa` suffix has an analogous friend in the C library called `atoi()` which converts an `ASCII` string to an integer.)

However, above functions were out of date. In modern ways, we use `pton`, `ntop`  instead.

p stands for `present` , n stands for `network`.

