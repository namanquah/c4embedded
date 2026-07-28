# Enumerated Types

Enumerated types are user-defined type that assigns readable names to a set of integer constants. It genereally makes the code more readable. `enum led {red, yellow, green, blue, white, black};` automatially makes red=0, yellow=1 and so on, black =5. 
Declare an enum variable (in C) as follows:
```c
enum led myled;
myled=yellow;
```
It can also be done in one step: `enum led myled=yellow;`

enums can be used wherever integers could have been used.

## Enumerated types and state machines

Using enums, it is very easy to develop and track states in a state machine

```c

int main(){
    enum led {red, yellow, green, blue, white, black};
    enum led next_led;      //declaration of next_led as an enum led
    next_led=red;
    for (int i=0; i<6; i++){    
        switch(next_led){
            case red:
                printf("red selected\n");
                next_led=green;
                break;
            case yellow:
                printf("yellow selected\n");
                next_led=blue;
                break;
            case green:
                printf("green selected\n");
                next_led=yellow;
                break;
            case blue:
                printf("blue selected\n");
                next_led=black;
                break;
            default:
                printf("other color\n");
                next_led=red;
        }
    }
}
```

The output of this will be: (not all enum states were used.)
```
red selected
green selected
yellow selected
blue selected
other color
red selected
```


Detetrmine the output of the following example:
```c
#include <stdio.h>
void washing_machine();
int main(){
    while(1){
        washing_machine();
    }
}

void washing_machine(){
    enum states {idle, filling, wash, drain, rinse,spin, stop};
    static enum states next_state=idle; //initialized in the declaration

    switch(next_state){
        case filling:
            printf("filling\n");
            next_state=wash;
            break;
        case wash:
            printf("washing\n");
            next_state=drain;
            break;
        case drain:
            printf("draining\n");
            next_state=rinse;
            break;
        case rinse:
            printf("rinsing\n");
            next_state=stop;
            break;
        case spin:
        default:
            printf("default state: stopped or idle. May restart\n");
            next_state=filling;
    }   
}
```

Can you confirm why the output will be the following? Note that the function is called repeatedly but this output seems to be differnt each time. Why?
```
default state: stopped or idle. May restart
filling
washing
draining
rinsing
default state: stopped or idle. May restart
filling
washing
....
```
<!-- 
Another example :
```c
#include <stdio.h>
int main(){
    enum states {wash, spin1, rinse1, spin2, dry, stop};
    enum states mystate;
    for(mystate=wash; mystate<=stop; mystate++)
        printf("current state=%d\n", mystate);
}
```

output:
```
current state=0
current state=1
current state=2
current state=3
current state=4
current state=5
```

-->
