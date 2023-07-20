# Number definition
The volume is divided into eight sections:

1. Commands
2. System calls
3. Subroutines
4. Special files
5. File formats and conventions
6. Games
7. Macro packages and language conventions
8. Maintenance

**Commands** are programs intended to be invoked directly by the user, in contradistinction to **subroutines**,
which are intended to be called by the user’s programs. Commands generally reside in directory /bin
(for bin ary programs). Some programs also reside in / usr/ bin, to save space in /bin. These directories
are searched automatically by the command interpreter.

# Quick start

Access the specific section of man page:
```bash
man 3 sleep
man 1 sleep
```

## Detail
1. `man man`

    See the man page for the man command with `man man`, and it shows the 9 sections as follows:
    DESCRIPTION
        man  is  the system's manual pager. Each page argument given
        to man is normally the name of a program, utility  or  func‐
        tion.   The  manual page associated with each of these argu‐
        ments is then found and displayed. A section,  if  provided,
        will  direct man to look only in that section of the manual.
        The default action is to search in all of the available sec‐
        tions following a pre-defined order ("1 n l 8 3 2 3posix 3pm
        3perl 5 4 9 6 7" by default, unless overridden by  the  SEC‐
        TION directive in /etc/manpath.config), and to show only the
        first page found, even if page exists in several sections.

        The table below shows the section numbers of the manual fol‐
        lowed by the types of pages they contain.

        1   Executable programs or shell commands
        2   System calls (functions provided by the kernel)
        3   Library calls (functions within program libraries)
        4   Special files (usually found in /dev)
        5   File formats and conventions eg /etc/passwd
        6   Games
        7   Miscellaneous  (including  macro  packages  and  conven‐
            tions), e.g. man(7), groff(7)
        8   System administration commands (usually only for root)
        9   Kernel routines [Non standard]

        A manual page consists of several sections.

2. `man <section_num> <cmd>`

    Let's imagine you are Googling around for Linux commands. You find the OPEN(2) pg online: open(2) — Linux manual page.

    To see this in the man pages on your pc, simply type in man 2 open.

    For FOPEN(3) use man 3 fopen, etc.

3. `man <section_num> intro`

    To read the intro pages to a section, type in man <section_num> intro, such as man 1 intro, man 2 intro, man 7 intro, etc.

    To view all man page intros in succession, one-after-the-other, do man -a intro. The intro page for Section 1 will open. Press q to quit, then press Enter to view the intro for Section 8. Press q to quit, then press Enter to view the intro for Section 3. Continue this process until done. Each time after hitting q, it'll take you back to the main terminal screen but you'll still be in an interactive prompt, and you'll see this line:

    `--Man-- next: intro(8) [ view (return) | skip (Ctrl-D) | quit (Ctrl-C) ]`