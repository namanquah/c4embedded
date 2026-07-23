# Control Structures

## If statements
General form:
``` c
if(cond){
    //actions
}
```

```c
if (a==b){
    //what to do
    printf("a is equal to b\n");
}

if (a!=b){
    //if a!=b
    printf("a is not b\n");
}else{
    //if condition is false
    printf("a is equal to b\n");
}
```
If statements can be nested and if statements can be chained eg if (cond)... else if (cond)... else if (cond) ... else...

## For Loops
General format:
```c
for (initalization; condition ; increment){
    //actions
}
```
Sequence of execution: 
1. initialization
2. check condition
3. if condition is false, exit block 
4. else: execution actions 
5. increment counter
6. Go to step 2


Examples
```c
for(int i=0; i<10; i++){
    //what has to be done 10 times

}
```

You can include a `break` to exit the for loop based on some condition, eg `if (a==4) break`

For loops can be nested eg
```c
for(int i=0; i<10; i++){
    for (int j=0; j<5; j++){
        printf("i is %d and j is %d\n", i, j);//this will run 50 times
    }
}
```

## While loops

General format: `while (condition) { .... }`

Example
```c
int i=0;
while (i<10){
    printf ("something\n");
    i++;
}
```

Note that if there is no way to change the condition, it will run for ever. example
```c
while(1){
    //done on thing
    //do another thing
}
```
The code above will run forever. It is freqently used in embedded systems because the code needs to run forexver and be ever ready to carry out tasks. Embedded Systems programs/firmware must never exit.

Another way of writing an infinite loop is
```c
for ( ; ;){
    //repeat this for ever
}
```


# Switch case
An alternative more structued way of writing chained if-else statements. It is also very useful for creating 'finite state machines'. Will revisit this topic again after disucssing the `enum` type

Example:
```c
int x=4;        //this could be any number based on runtime conditions
switch (x){
    case 1: printf("x is one\n");
            break;
    case 2: printf("x is two\n");
            printf("x is also even\n");
            break;
    case 3: printf("x is three and prime\n");
            break;
    default: printf("not a number between 1 and 3\n");    
}
```

If the `break` is missing, it will cause subseqent statements to executed even if not for that case.

# Examples
Determine the output of the following code snippet. Determine it manually (before you ever consider running the code on say onlinegdb.com)

```c
/**
* basic C control structures (while, for, switch)
* variable sizes, working with uint8_t etc
*/


#include <stdio.h>
#include <stdint.h>

int main()
{

int8_t x;
x=200;
printf("x = %d, %X\n", x, x);

int i=0;
for( ; ; ){
    printf("%d\n", i);
    i++;
    if (i==9) break;
}


while(1){
    printf("in the while loop\n");
    if (i==9) break;
}
 


switch (i){
    case 0: printf("i is zero"); 
    break;
    case 9: printf("this is 9\n");
    case 10:
    case 11: printf("this is 11\n");
    break;
    default:
        printf("non of the above\n");
}

   return 0;
}


```

<!-- add code that runs in a loop say 10 times and runs a switch case statemtn. students to determine output
set up next_state to be the swithc variable >