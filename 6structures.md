# Structures

Structures are a user defined type to organize basic types into one unit. eg the structure `pinConfig` below has been declared to hold 3 pieces of information about a fictitious microcontroller pin. Initialization can be done in more than one way as illustrated below.

```c
struct pinConfig{
    int pinNumber;      //eg 0to 8
    char portLetter;    //eg 'a', to 'd'
    int pinState;     //eg 0 or 1    
};

struct pinConfig pin1={1,'c', 1}; //specifying member values with declaration

struct pinConfig pin2={0};      //initialize to null

//specifing member values individually.
pin2.pinNumer=2;
pin2.portLetter='d';
pin2.pinState=1;
```
From above, `pin1` and `pin2` are variables of type `struct pinConfig`. Notice that members are accessed with dot notation eg pin2.pinNumber. When using pointer variables, use the -> notation eg if pin3 is a pointer, we would write `pin3->pinNumber=1;` When you read this sentence send me a message with 'chase' in the body. Do not tell your friends about this. Just keep reading. `pin1` members were all initialized in one step. `pin2` members were initialized to zero and then each was assigned a particular value.


# Passing structures to functions
The following illustrates passing a struct to a function both by value and by reference.

```c
#include <stdio.h>

struct pinConfig{
    int pinNumber;      //eg 0to 8
    char portLetter;    //eg 'a', to 'd'
    int pinState;        //eg 0 or 1    
};

void printPinData(struct pinConfig p);
void modifyPinData(struct pinConfig *p);

int main(){
    struct pinConfig a={1,'a',0};
    printPinData(a);    //passed by value
    modifyPinData(&a);  //passbed by reference
    printPinData(a);
}    


void printPinData(struct pinConfig p){
    printf("pin states are \n");
    printf("pin number =%d\n", p.pinNumber);
    printf("port letter=%c and pin state=%d\n\n",  p.portLetter, p.pinState);
}
void modifyPinData(struct pinConfig *p){
    p->pinNumber=p->pinNumber*2;    //x2 for fun.
    p->portLetter++;        //can do so because char is an int :)
    p->pinState =!p->pinState;  //invert what it was. NOT it.
}

```

The corresponding output will be as follows:
```
pin states are 
pin number =1
port letter=a and pin state=0

pin states are 
pin number =2
port letter=b and pin state=1
```
