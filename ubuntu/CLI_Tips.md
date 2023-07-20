### which & type

Which only works for executable programs, not builtins nor aliases that are substitutes for actual executable programs. When we try to use Which on a **shell builtin** for example, `cd`, we either get no response or get an error message.

### whatis

The `whatis` program displays the name and a one-line description of a man page matching a specified keyword:

```C
$ whatis rsync
rsync (1)            - a fast, versatile, remote (and local) file-copying tool
```

### grep - Print Lines Matching a Pattern

`grep ` is used to find text patterns within files. It used like this:

```bash
grep pattern [file...]
```

The advanced patterns is called `regular expressions` .



### sleep

Adding the `-e` option to `echo` will enable interpretation of escape sequences.

We can create a primitive countdown timer:

```bash
sleep 10; echo -e "Time's up\a"
```



 ### Searching History

At any time, we can view the contents of  the history list by doing the following:

```bash
history | less
```

Let's say we want to find the commands we used to list `/usr/bin`. This is one way we could do this:

```bash
history | grep /usr/bin
```

And let's say that among our results we got a line containing an interesting command like this:

```bash
88 ls -l /usr/bin > ls-output.txt
```

The `88` is the line number of the command in the history list. We could use this immediately using another type of expansion called `history expansion`.

To use our discovered line, we could do this:

```bash
!88
```

bash will expand !88 into the contents of the 88th line in the history list.



## Regular Expression



### Metacharacters and Literals



Specify the number of times an element is matched.

**example**:

We considered a phone number to be valid if it matched either of these two forms, where `n` is a numeral:

`(nnn) nnn-nnnn`

`nnn nnn-nnnn`





















