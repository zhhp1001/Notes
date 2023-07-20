

The first rule seen by make is used as the *default rule*. A *rule* consists of three parts: 

- the target

  > the file or thing that must be made.

- its prerequisites

  > those files that must exist before the target can be successfully created.

- the command(s) to perform

  > those shell commands that will create the target from the prerequisites.

```makefile
target: prereq1 prereq2
	commands
```

`makefiles` are written *top-down* but the commands are executed bottom-up.

### Variables Used by Implicit Rules

[Reference](https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html)

**Automatic Variables**

7 "core" automatic variables:

`$@` The filename representing the target

`$%` The filename element of an archive member specification

`$<` The filename of the first prerequisite.

`$?` The names of all prerequisites that are newer than the target, separated by spaces.

`$^` The filenames of all prerequisites, separated by spaces. This list has duplicate filenames removed since for most uses, such as compiling, copying, etc., duplicates are not wanted.

`$+` Similar to `$^`, this is the names of all the prerequisites separated by spaces, except that `$+` includes duplicates. This variable was created for specific situations such as arguments to linkers where duplicate values have meaning.

`$*` The stem of the target filename. A stem is typically a filename without its suffix. (We'll discuss how stems are computed later in the section "Pattern Rules.") Its use outside of patter rule i discouraged.

`$(@D)` The directory part of the file name of the target, with the trailing slash removed. If the value of `$@` is `dir/foo.o` then `$(@D)` is `dir`. This value is `.` if `$@` does not contain a slash. 

## Rules

1. *Explicit rules* use explicit filenames
2. *Pattern rules*  use wildcards instead of explicit filenames.
3. *Implicit rules*
4. *Static pattern rules* are like regular pattern rules except they apply only to a specific list of target files.

### Phony Targets

Any targets can be declared phony by including it as a prerequisite of `.PHONY`

```makefile
.Phony: clean
clean:
		rm -f *.o lexer.c
```

Phony targets can also be thought of as `shell scripts` embedded in a `makefile`

 ### The Patterns

The percent character `%` in a pattern rule is roughly equivalent to `*` in a Unix shell. 



## Variables and Macros

### Types of Assignment

`=`  for creating recursive variables. 

`:=`  for creating simple variables.

`?=`  This operator will perform the requested variable assignment only if the variable does not yet have a value.

`+=`  is usually referred to as append.



### Macros

A *macro* is just another way of defining a variable in make, and one that can contain embedded newlines! The GNU make manual seems to use the words *variable* and *macro* interchangeably.



#### The use of @ 

- Command Modifiers in Chapter 5...



### Conditional and include Processing

Parts of a `makefile`  can be omitted or selected while the `makefile` is being read using *conditional processing directives*. The condition that controls the selection can have several forms such as `is defined` or `is equal to` .

The *if-condition* can be one of:

- `ifdef `variable-name
- `ifndef` variable-name
- `ifeq` test
- `ifneq` test

## Functions

A function invocation looks much like a variable reference, but includes one or more parameters separated by commas. A user-defined function is stored in a variable or macro and expects one or more parameters to be passed by the caller.



## Include 顺序也会影响结果...

