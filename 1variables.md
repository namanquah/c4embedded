# Variables

Use variables to hold a value. The type of variable must be specified. The main type are 
* `int`   - eg 10
* `float` - eg 3.142
* `char`  -for single characters eg 'a', and special characters like '\n' , the newline character

To print a variable in a `printf()` statement, a format specified is included as a place holder in the string to print. The variable to print is suppiled after the string to print, after a comma.

The placeholder are as follows
| Type | format specifier |
|------|------------------|
| int  |  %d              |
|float |  %f              |
|char  |  %c              |

```c
#include <stdint.h>

int main(){
    int a=4;
    float b=3.5;
    char c='d';    
    printf("The value of a is %d\n");
    printf("The values of b=%f and c=%c\r\n", b, c);
    
    //\r and \n are for carriage return and newline, causes text to go to new line
}

```


## Bits, Binary, HEX and Fixed size integer variables


Know this, especially the conversion from BIN to HEX and vice-versa for at least 0-15. Hex numbers are usually written preceeded by 0x eg 15DEC or 1111BIN is 0xF (in HEX) 


| Number (Decimal) | Binary | Hexadecimal |
| :---: | :--- | :---: |
| **0** | 0000 | 0 |
| **1** | 0001 | 1 |
| **2** | 0010 | 2 |
| **3** | 0011 | 3 |
| **4** | 0100 | 4 |
| **5** | 0101 | 5 |
| **6** | 0110 | 6 |
| **7** | 0111 | 7 |
| **8** | 1000 | 8 |
| **9** | 1001 | 9 |
| **10** | 1010 | A |
| **11** | 1011 | B |
| **12** | 1100 | C |
| **13** | 1101 | D |
| **14** | 1110 | E |
| **15** | 1111 | F |

Some easy things to rembemer: 
* 10 is **1010**        ten-ten
* 11 is the number afterwars ie 10 11
* 7 is 111
* 15 is 1111
* 14 is double 1110 (shift numbers left to double); just as 5 is 101, ten is 5 shifted left
* 6 is 110, and 12 is 1100; 13 is the next number 1101
* just know the rest, 9 is 1001

Given any base 10(deicmal) number you can convert to HEX or BIN with say a calculator (or other means). Given a HEX number, you can convert to BIN quckly by writing out each number as its equivalent 4-bit number. Examples:

|HEX.     | Binary Equivalent   |
|-------- | --------------------|
| 0xF1A3  | 1111 0001 1010 0011 |
| 0x1C01  | 0001 1100 0000 0001 |


These two numbers above are all 16-bits long (2 bytes each)

_An integer may be 4 bytes long (or 2, depending on the hardware archtecture)_

The `int` type on the STM32 (and ARM processors) is 4 bytes. If we wish to store a number in exactly 8 or 16 bits, a differnt type can be used. For that, include _stdint.h_, which has the appropriate definitions. They key types are as follows:

| Type      | description|
|-----------|-----------------------|
|uint8_t    |Unsigned 8-bit integer |
|int8_t     |Signed 8-bit integer |
|uint16_t   |Unsigned 16-bit integer |
|int16_t    | Signed 16-bit integer |
| etc..     |  |

It is avaialbe for 8, 16, 32, 64 etc

```c
#include <stdint.h>
#include <stdio.h>

int main(){
    int a=0xF1A31C01;       //this will be stored correct as 4 bytes/32 bits on ARM Cortex microcontroller
    uint16_t b= 0x1234;     //stored correctly as 2 bytes/16bits
    uint8_t c=0x12;         //stored correctly as 1 byte/8 bits
    uint8_t d=0xF1A31C01;   //this will be truncated, only lowest 8 bits are stored, 
                            //only 0x01 stored, it will also generate a warning 

    printf ("a=%X  b=%X c=%x and d=%X\n", a, b, c, d);
    //the %X is a placeholder for HEX, 
}

```

the output will be
``` 
a=F1A31C01  b=1234 c=12 and d=1
```

As an aside: to cure the warning that may be generated on the line `uint8_t d=0xF1A31C01;` do a "cast" to convert from one compatible type to antoher as follows: `uint8_t d= (uint8_t)0xF1A31C01;`. Still, only 0x01 will be stored, but without a warning.

There is a consequence of storing a large number in a small size. It gets truncated. 
1. Thee largest number that can be stored in uint8_t is 255.
2. If it is stored in a **signed** type, then if the first bit is 1, it will a negative number, stored in _two's complement notation_. The `int8_t` type stores numbers from -128 to +127

---
# Examples

## Example 1. Basic printing and variable sizes

Determine the output of the following code snippet. Note: `'\t'` character is used to add a tab/space. Also `%b` is a format specifier allowed on some versions of C, that prints in binary form. You may run this code on [onlinedgb.com](onlinegdb.com) to see how it behaves **after** you have evaluated by paper and pen.

```c

#include <stdio.h>
#include <stdint.h>

int main()
{
    printf("Hello World");
    int a;
    a=12;
    printf("\nvalue of a is %d \t %X  %b\n", a, a, a);

    uint8_t b;
    b=255;
    b=b+45;     //should be 300
    //b=300;
    printf("value of b is %d  %b\n", b, b);
    
    int8_t c;
    c=255;
    printf("value of c is %d  %b\n", c, c);
    
    char x='s';
    printf("the character and previous number are %c and %d", x,c);
    
   return 0;
}

```

