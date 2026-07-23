# Macros & Bitwise Operations

## Basic Macros

Macros are a names that represent a value or a fragment of code that is given a symbolic name. They are declare in the form `#define SYMBOLIC_NAME value`

eg
```c
#define MULTIPLIER  4.321
#define SIZE        10
#define SQR(X)      (X*X)
#define MASK(X)     (1<<X)
#define TRUE        1
#define ONEBIT      1
#define SHIFT(X)    (ONEBIT<<X)             //defined in terms of another Macro
```

Note the absence of semicolons ; becuase after subsitution (by a pre-processor, and before compilation takes place) the updated code should read correct and by syntatically correct. Macros can take a parameter. SQR(3) will be evaluted to 3*3. Similarly MASK(3) will be replaced with (1<<3). _Note that these are NOT functions._

Also note that these are not "constant". In c, to define a constant, use the keyword `const` in front of the declaration eg
```c
const float pi 3.142;
```


## Bitwise operations
It is generally needed to set and clear individual bits of a bit-pattern stored in a regsiter (memory location). Why will this arise? Say 8 pins on a microcontroller may be mapped to 8 bits in a register, and we want to turn on some of the pins (by making the bits 1) or turn off some pins by making the bits 0. It could also be that we sets of 4 bits are used to configure a pin in a particular way. I may need to set a subset of 4 bits to a particular value to for example make a pin an input pin or output pin. Bitwise operations should enable me to set, clear, toggle or even determine what was previously set.

Bit positions in a register are counted from 0 at the Least Significant Bit position.

### Set a bit
If `reg` is a register with the value 0xA0 (ie 1010 0000 BIN ) we can set bit 2 to 1 as follows
```c
// all of the following are equivalent
reg = reg | (0x4);      //OR'ing with 0000 0100
reg = reg | 4;          //this 4 is DEC, but same value as 0x04
reg = reg | (1<<2)      // (1<<2) is same as 100BIN
reg |= (1<<2);          //short hand for above,  commonly seen
reg |= MASK(2);         //using the MASK definition given above,  commonly seen
```

Multiple bits can be set at once. Eg to set bits 2,3 and 4
```c
reg |= MASK(4) | MASK(3) | MASK(2);
reg|= (7<<2);       //this will shift 111BIB left by 2, ie 11100
```

### Clear a bit
To clear a bit the operation is to AND a NOT of the MASK
To cearl bit 2 of reg, the following are equivalent:
```c
reg = reg & ~(0x4);
reg = reg & ~4;
reg = reg & ~(1<<2);
reg& = ~(1<<2);         // commonly seen
reg& = ~MASK(2);        // commonly seen
```

Multiple bits can be cleared at once. Eg to clear bits 2,3 and 4
```c
reg &= ~(MASK(4) | MASK(3) | MASK(2));  //pay attention to brackets!
reg&= ~(7<<2);                          //this will shift 111BIN left by 2, ie 11100
```

### Toggle a bit
A toggled bit becomes the inverse of itself. Use the XOR (carat) operation
eg to toggle bits 2,3 and 4:
```c
reg ^= (MASK(4) | MASK(3) | MASK(2));
reg^= (7<<2);

```
### Determining value of a bit
To determine the value of bit 2:
```c
int val= (reg>>2) & 1;      

```
The operation will first shift the value in reg and move the desired value to position 0. Then we AND it with 1 (ie 0000 0001). The result is a singular bit which will be a zero or a 1. If you have read up to this point, send me a message 'alpha' by whatsapp or email etc. Do not tell your mates about this. Am checking who is reading. Just keep reading. Where might this be used? A button press or a sensor connected to a pin may generate a 1/HIGH when activated. How do we know it is a HIGH and take action? We can write a simple conditinal statement as follows:

```c
if ((reg>>2) & 1) { //means it is a HIGH
    //do something if bit in position 2 is 1
}else {
    //do other thing if it is zero
}
```



<!--  Using Macros for conditional compilation
Where a block of code should be excluded from compilation, it is possible to make use of conditional macros. For example to include a block of code for compilation,  -->

# Examples
