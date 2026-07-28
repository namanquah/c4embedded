# Arrays

Arrays are a collection of similar types that be indexed.

Instead of declaring ten variables of type int eg 
```c
int a, b, c,d,e,f,g,h, i,j;
```
we would instead do `int A[10]` where `A[0]` up to `A[9]` represent the 10 integers.  This is a *list* of 10 integers.

A table of 10 x 4 integers will be defined a `int A[10][4]`.

When passing an array to a function simply pass the name of the Array. It is treated as a refernce. _The name of an array is a pointer (to the first element)_.

# Example usage:
Note alternative ways of declering and initializing an array below. Also arrays are not 'objects' so they do not know their size/length. When passing to an array to a function, pass the size of the array as well.

```c
#include <stdio.h>

#define Q_SIZE 5
void printArray(int A[], int size);
void doubleArray(int A[], int size);
int main(){
    int Q[Q_SIZE];  //Q is an array of 5 integers
    Q[0]=10;        //assign values individually as needed.
    Q[1]=9;
    Q[2]=8;
    Q[3]=7;
    Q[4]=6;
    
    //B is an array of 10 elements, size determined by no of elements initialized
    int B[]={2,2,4,4,6,6,8,8,10,10}; //initialized with declaration.
    
    //print Q
    printf("=====Q======\n");
    printArray(Q, Q_SIZE);  //Q_SIZE was defined earlier.
    doubleArray(Q, Q_SIZE); //pass by ref; note that &Q is not used.
    printf("=====doubled Q======\n");
    printArray(Q, Q_SIZE);      
    //print B also
    printf("=====B======\n");
    printArray(B,10);
}

void printArray(int A[], int size){
    for (int i=0; i<size; i++)
        printf("Element[%d]=%d\n", i, A[i]);
}
void doubleArray(int A[], int size){
    for (int i=0; i<size; i++)
        A[i]=A[i]*2;
}
```

The output will be as follows:
```
=====Q======
Element[0]=10
Element[1]=9
Element[2]=8
Element[3]=7
Element[4]=6
=====doubled Q======
Element[0]=20
Element[1]=18
Element[2]=16
Element[3]=14
Element[4]=12
=====B======
Element[0]=2
Element[1]=2
Element[2]=4
Element[3]=4
Element[4]=6
Element[5]=6
Element[6]=8
Element[7]=8
Element[8]=10
Element[9]=10
```