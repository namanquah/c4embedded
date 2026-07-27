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