# getopt()



## optstring



​	It is just a string, and each character of this string represents an option. If this option requires an argument, you have to follow the option character by `:`.

​	For example, `"cdf:g"` accepts the options `c`, `d`, `f`, and `g`; `f` requires an additional argument.

An option in command line looks like `-option`, so you can use the options `-c`, `-d`, `-f argument` and `-g`.

​	When the option has an argument, the value is found in the (global) variable **optarg** that's declared in the header where [`getopt()`](http://pubs.opengroup.org/onlinepubs/9699919799/functions/getopt.html) is declared (``). Two colons is an extension that indicates the following argument is optional. 

>- The string itself is used for specifying the legal options that can appear on the commandline,
>- If the option is followed by a `:`, then that option has a required parameter - not specifying it will cause the function to fail,
>- If the option is followed by a `::`, then that option has an optional parameter.