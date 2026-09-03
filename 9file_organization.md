# Conditional compilation
A block of code may be included or excluded from compilation by using conditional macro directives. The code snipet  `printf("something special prints here\n"); ...` in the block below will not be compiled because `SPECIAL_CODE` has not been defined prior

```c
#ifdef SPECIAL_CODE
    printf("something special prints here\n");
    //..additional lineks
#endif 
```

To have this included in the complilation, we must include the following line before the block
```c
#define SPECIAL_CODE
```

# File Organization

Until now, we kept all function prototypes, #defines (macros) and global variables before the main() funciton and then we keep the function implementation later in the main file.

There is a better way of organizing the code as the project increases in size.

1. First move all related function prototypes, #defines (macros) and global variables  to a file with a .h extension as a header file. This will become a library you can share with others. eg as a driver file header.
2. Keep all function implementations corresponding to the function prototypes in a file with a .c extension. (using same name is the convention)
3. Keep the main file to run in a .c file. This will be the only file with a main() function

There will be multiple header files and multiple corresponding implementation files.

Import the .h file into both its implementation .c as well as the file with the main() function. This is illustrated below.


### Example file with main
This example uses code from the section on functions covered earlier. This file can have any name. Commonly it may be named `main.c`
```c
#include <stdio.h>
#include <file1.h>

int main(){
    int result=0;
    int x=4;
    int y=5;
    printf("before call: value of x=%d  y=%d res=%d\n",x,y,result);
    result=special_addition(x,&y);      
    printf("after call: value of x=%d  y=%d res=%d\n",x,y,result);    
}
```

### Example header file

The example header file is saved in a file named `file1.h`
A few notes:
- Since there may be multiple "libraries"  of .h and .c pairs created, it is quite likely that one library may #include another library and the main will also include the same library. To prevent errors as a result of this kind of duplicated imports, we place an "include guard" in each header file, to prevent the compiler from including it twice.

In this case, it is #ifndef FILE1_H, then we #define it so it cannot be included subsequently. (it is only included when it has not been previously defined, which is once)

```c
#ifndef FILE1_H
#define FILE1_H

int  special_addition(int a, int *b);   
//add other function definitions, structs, enums etc as needed.

#endif
```

It is customary to name the include guard the same as the file name eg `FILE1_H` for `file.h`

### Example implmentation file
This file is saved in `file1.c` to match its header `file1.h`
```c

#include "file1.h"

int  special_addition(int a, int *b){   
    printf("\t In func: before operation: values: a=%d  b=%d\n",a,*b);
    a=a*2;
    *b= *b * 2;     //note use of *b 
    printf("\t In func: after operation: values: a=%d  b=%d\n",a,*b);
    return a+ *b;
}

//add other function implmentations
```

Do note that the .c file is not included in the main file.

