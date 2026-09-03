# Dynamic Memory Allocation

These are topics we may use only briefly but you can explore

To have memory allocated to a type, you must ask for the memory, check if it was allocated, used it and then free it up.

Illustrating with a trivial example of creating memory for the type `int`, but this works for struct, arrays and any other types

```c
#include <stdio.h>   
#include <stdlib.h>  // Required for malloc() and free()

int main() {
    int *oneInt;    //declare as a pointer to the type
    oneInt=(int*) malloc(sizeof(int));
    if (oneInt==NULL)   //check
        return 1; //failed, return error code
    *oneInt=4;      //use the variable
    printf("Value is %d\n", *oneInt);
    free(oneInt);       //deallocate the memory
    oneInt=NULL;    // Clear pointer to avoid a dangling reference
    
    
    //Creating an array of 3
    int *arr = (int*) malloc(3 * sizeof(int));
    if (arr == NULL) //check
        return 1; 
    //Use array as normal
    arr[0] = 100;
    arr[1] = 200;
    arr[2] = 300;
    for (int i=0; i<3; i++)
        printf("Arry[%d]: %d\n", i,arr[i]);

    free(arr);      //deallocate, not 3 x
    arr = NULL; // Clear pointer to avoid a dangling reference
    return 0;
}
```

Output will be
```
Value is 4
Arry[0]: 100
Arry[1]: 200
Arry[2]: 300
```

