#C programming tutorial

This is an abridged version of my appendix on C programming. This will be a mix of totorial and brief exercises to try.

To run C programs, a compiler is needed. YOu may install VSCode as an editor and include a C extension, or simply visit [online GDB] (https://www.onlinegdb.com/) to execute code without installing anything.  For online gdb, do select C as the language.


##first program: _Hello World!_
The first program to excute is a hello world program 

It will look as follows:

```c
/*  This is a multi-line comment
    It is ignored completely
    The program starts below. */

#include <stdio.h>

int main()        //this is also a comment, showing where the program starts
{
    printf("Hello World");

    return 0;
}

```
The key elements of the program are as follows: 
* Program starts from main() which is a function, and executes sequentially. The function is expeced to return an integer (int)
* printf() is a function to print the string/text passed to it (not quite available in embedded systems as there is not screen)
* program ends by returning a value of 0.

Note that statements end with a semicolon ; and the contents of the function is enclosed in the block bounded by { and }
Run this and see output

---

#Hello world ++
