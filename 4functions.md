# Functions

Orgnaize code in reusable blocks of fuctions.

## Basic function
Functions may have no parameters. They may have internal variables known only within the scope of the function. Functions "prototypes" must be declared before they are first called. They may return some type (eg int, float etc) or void. 

```c
#include <stdio.h>

void custom_print();        //this is the function prototype or definition

int main()
{
    printf("Hello World\n");
    custom_print();         //a call to the function
    printf("done\n");

    return 0;
}

void custom_print(){        //function implementation
    int x=4;
    for (int i=0; i<x; i++){
        printf("HELLO # %d\n", i);
    }
}
```

Output will be as follows:
```
Hello World
HELLO # 0
HELLO # 1
HELLO # 2
HELLO # 3
done
```

## Funcitons with parameters
Functions may take parameters and may return a value

```c
#include <stdio.h>

int  add_two_numbers(int a, int b);

int main()
{
    int sum=0;
    for (int i=0; i<3; i++){
        sum=add_two_numbers(i, 10); 
        printf("sum of %d and 10 is %d\n",i, sum);
    }
    return 0;
}

int  add_two_numbers(int a, int b){
    int c=0;
    c=a+b;
    return c;
}
```
The output will be:

```
sum of 0 and 10 is 10
sum of 1 and 10 is 11
sum of 2 and 10 is 12
```

## Passing parametes by Value
Functions may modify values passed this way, but do not impact variables in the calling function. In this case main() is the calling function it has its own copy of the variables.

```c
#include <stdio.h>
int  special_addition(int a, int b);
int main(){
    int result=0;
    int x=4;
    int y=5;
    printf("before call: value of x=%d  y=%d res=%d\n",x,y,result);
    result=special_addition(x,y);
    printf("after call: value of x=%d  y=%d res=%d\n",x,y,result);
}

int  special_addition(int a, int b){
    printf("\t In func: before operation: values: a=%d  b=%d\n",a,b);
    a=a*2;
    b= b * 2;
    printf("\t In func: after operation: values: a=%d  b=%d\n",a,b);
    return a+ b;
}

```


Study this output carefully. Key notes:
1. x and y are mapped onto the a and b in the special function. A "copy" of the values are passed to the funciton. Though the called function special_additon() modifies the copy during operation, the original value in the caller function (main) are not altered. This is called "passing by value"


Output is as follows:
```
before call: value of x=4  y=5 res=0
         In func: before operation: values: a=4  b=5
         In func: after operation: values: a=8  b=10
after call: value of x=4  y=5 res=18
```

## Passing parametes by Reference
A small change to the previous program enables a called function to permanently modify parameters passed to it. - by passing a reference to the original variables.
Key notes:
1. For a function to receive parameters by **reference**, the variable name should be specified with __*__ in front of it.
2. When calling the function, pass the *reference* or *address* by preceeding the variable name with an __&__ (ampersand).


```c
#include <stdio.h>
int  special_addition(int a, int *b);   //b is a pointer. It expects a reference to be passed
int main(){
    int result=0;
    int x=4;
    int y=5;
    printf("before call: value of x=%d  y=%d res=%d\n",x,y,result);
    result=special_addition(x,&y);      //notice use of & in the function call.
    printf("after call: value of x=%d  y=%d res=%d\n",x,y,result);
}

//b is expecting a reference to an int to be passed to it
//b is a "pointer variable. Pass a reference/address/pointer to it.
int  special_addition(int a, int *b){   
    //use *b to dereference the pointer, to get the actual int
    printf("\t In func: before operation: values: a=%d  b=%d\n",a,*b);
    a=a*2;
    *b= *b * 2;     //note use of *b 
    printf("\t In func: after operation: values: a=%d  b=%d\n",a,*b);
    return a+ *b;
}
```


1. In the function prototype `int  special_addition(int a, int *b)`, b is declared as a pointer.
2. `b` variable is not an integer but a reference to an integer. (also called a pointer to an integer)
3. Within the function b is *dereferenced* and used as `*b` eg `*b= *b * 2;` It could equally be written without spacing eg `*b=*b*2;`
4. `*b` is a 'dereferenced' integer pointer, and refers to the actual int.

The output is as follows:
```
before call: value of x=4  y=5 res=0
         In func: before operation: values: a=4  b=5
         In func: after operation: values: a=8  b=10
after call: value of x=4  y=10 res=18
```

Note clearly that this time, the value of y in the main has been modified (whereas x which was still passed by value has not been modifed). If you have read this sentence send me the message 'bisect' and do not tell anyone in the class about this. Am just checking who is reading. Keep reading. By making use of multiple pointer variables as parameters, we can make a function modify more than one variable.



 ## Static variables
 When a variable is qualified as static in *a function*, it is initialized only once and remembers its value between function calls.

 ```c
#include <stdio.h>
void countup_v1(void);
void countup_v2(void);

int main(){
    for (int i=0; i<3; i++)
        countup_v1();
    for (int i=0; i<3; i++)
        countup_v2();
    
}
void countup_v1(void){
    int x=0;
    x++;
    printf("v1: current x=%d\n",x);
}
void countup_v2(void){
    static int x=0;     //qualified as static
    x++;
    printf("v2: current x=%d\n",x);
}
 ```

The output will be as follows:
```
v1: current x=1
v1: current x=1
v1: current x=1
v2: current x=1
v2: current x=2
v2: current x=3
```


## Summary:
- Function variables are local to the function
- Variables in the function prototype can be used in the funciton and are known only in the function 
- When parameters are passed by value, modificaitons within the function do not affect the original variables passed.
- When paramters are passed by reference, the modification directly change the original variables.
- Function calls that pass parameters by reference run faster and use less memory 
- Functions may call other functions
- Static variables in a function are initialized only once! They return their value even after a function has exited/gone out of scope.



## Evaluate
Examine the following function declarations
```c
int fxn1(int x, int y, int z);
void fxn2(int a, int *b, int *c);
```

Examine also the following variable definitions
```c
int p,q,r;
int result;
p=3;q=4; r=5;

```

- What is the correct way to call the function `fxn1` with p,q and r? (assign returned value to the variable named “result”)
- will there be an error compiling if the returned value from the function is not assigned to a variable?
- What is the correct way to call the functions `fxn2` with p,q and r?
