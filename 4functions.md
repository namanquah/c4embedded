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
Parameters passed this way do not impact variables in the calling function. In this case main() is the calling function and main() has its own variables.

```c
#include <stdio.h>
int  special_addition(int a, int b);
int main(){
    int result=0;
    int x=4;
    int y=5;
    int a=40;
    int b=50;
    printf("before call: value of x=%d  y=%d res=%d\n",x,y,result);
    result=special_addition(x,y);
    printf("after call: value of x=%d  y=%d res=%d\n",x,y,result);
    
    printf("-------------\n");
    result=0;
    printf("before call: value of a=%d  b=%d res=%d\n",a,b,result);
    result=special_addition(a, b);
    printf("after call: value of a=%d  b=%d res=%d\n",a,b,result);
}


int  special_addition(int a, int b){
    printf("\t In func: before operation: values: a=%d  b=%d\n",a,b);
    a=a*2;
    b=b*2;
    printf("\t In func: after operation: values: a=%d  b=%d\n",a,b);
    return a+b;
    
}
```

Study this output carefully. Key notes:
1. x and y are mapped onto the a and b in the special function. A "copy" of the values are passed to the funciton. Though the called function (special_additon) modifies the copy during operation, the original value in the caller function (main) are not altered
2. a=40 and b=50 in the main() are passed to the special_addition() function. That a and b are NOT the same as the ones in the special function though their names are identical. As before, they are passed by value i.e. a 'copy' is passed to the called function and modifications do not affect the original


Output is as follows:
```
before call: value of x=4  y=5 res=0
         In func: before operation: values: a=4  b=5
         In func: after operation: values: a=8  b=10
after call: value of x=4  y=5 res=18
-------------
before call: value of a=40  b=50 res=0
         In func: before operation: values: a=40  b=50
         In func: after operation: values: a=80  b=100
after call: value of a=40  b=50 res=180
```

## Passing parametes by Reference
A small change to the previous program enables a called function to permanently modify parameters passed to it. - by passing a reference to the original variables.
Key notes:
1. For a function to receive parameters by **reference**, the variable name should be specified with __*__ in front of it.
2. When calling the function, pass the *reference* or *address* by preceeding the variable name with an __&__ (ampersand).


```c
#include <stdio.h>
int  special_addition(int a, int *b);       //b will be expecting reference; b is a "pointer"
int main(){
    int result=0;
    int x=4;
    int y=5;
    int a=40;
    int b=50;
    printf("before call: value of x=%d  y=%d res=%d\n",x,y,result);
    result=special_addition(x,&y);          //note that y is being passed by reference. Its address
    printf("after call: value of x=%d  y=%d res=%d\n",x,y,result);
    
    printf("-------------\n");
    result=0;
    printf("before call: value of a=%d  b=%d res=%d\n",a,b,result);
    result=special_addition(a, &b);
    printf("after call: value of a=%d  b=%d res=%d\n",a,b,result);
}


int  special_addition(int a, int *b){       //in the funciton, use *b to obtain the value
    printf("\t In func: before operation: values: a=%d  b=%d\n",a,*b);
    a=a*2;
    *b= *b * 2;
    printf("\t In func: after operation: values: a=%d  b=%d\n",a,*b);
    return a+ *b;
    
}

```
1. In the function prototype `int  special_addition(int a, int *b)`, b is declared as a reference.
2. `b` variable is not an integer but a reference to an integer. (also called a pointer to an integer)
3. Within the function b is *derefernced* and used as `*b` eg `*b= *b * 2;`
4. `*b` is a 'dereferenced' integer pointer, and refers to the actual int.

<!--
consider simplifying the example and removing duplication parameter names
 -->


 ## Static variables
 When a variable is qualified as static in *a function*, it is initialized only once and remembers its value between function call.

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

<!-->
# Exercise 1
Determine the output of the following piece of code: FSM. defere until enum
-->

## Summary:
- Function variables are local to the function
- Variables in the function prototype can be used in the funciton and are known only in the function 
- When parameters are passed by value, modificaitons within the function do not affect the original variables passed.
- When paramters are passed by reference, the modification directly change the original variables.
- Function calls that pass parameters by reference run faster and use less memory 
- Functions may call other functions
- Static variables in a function are intialized only once!They return their value even after a function has exited/gone out of scope.




