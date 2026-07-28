# Strings
C has no native string type, instead an array of characters. `"Nathan"` is a string (double quotes), but stored as 
```c
'N','a','t','h','a','n','\0'
```
There are 8 distinct charcters, the last charcter '\0' is the null terminating character. Characters are processed as part of the string until this charcater is encoutered.

Strings can be defined in two ways, with differnt consequneces. When declared as an array of `char`, eg `char fname[]={'K','o','f','i','\0'};` each character can be changed like in a normal array. If declared as a pointer to `char`, then it is immutable (unchangeable). eg `char *surname="Mensah";`

```c
#include <stdio.h>
int main(){
    char fname[]={'K','o','f','i','\0'};    //this is changeable
    char *surname="Mensah";         //this is readonly
    

    //%s is the placeholder for printing strings
    printf("Surname is %s\n", surname); //* is not used; 
    printf("Firstname is %s\n", fname);
    
    fname[0]='Y';       //changing first char.
    printf("New firstname is %s\n", fname);     
}
```

Outupt will be:
```
Surname is Mensah
Firstname is Kofi
New firstname is Yofi
```

Notes: many functions expect a pointer to char ie `char *`. For all those simply provide the name of the array or the name of the variable declared as pointer to char.

# Using string functions
It is often neccessary to compose stirngs and display them say on an LCD/terminal, or save in a log. In that case, create a char array as a string buffer and write/print into it, and then display as needed. The example below copies two names into one space using differnt methods. The `strcpy()` and `strcat()` functions need the `<string.h>` library is needed and thus included.

```c
#include <stdio.h>
#include <string.h>

int main(){
    char fname[]={'K','o','f','i','\0'};    //this is changeable
    char *surname="Mensah";     //this is readonly
    char buff[80];              //big enough buffer
    
    
    strcpy(buff,fname);     //copy fname string into buff.
    printf("1. text in buff is %s\n", buff);
    
    strcat(buff," ");      //concatenate one space as string (not char)
    strcat(buff,surname);      //concatenate surname string to what was there.
    printf("2. text in buff is %s\n", buff);
    
    //using sprintf function: -allows us to format, as with printf
    //if you read this comment, send me message that says
    //'delta', and tell no one about it. Keep reading.
    sprintf(buff, "Surname is %s and first name is %s\n", surname, fname); //* is not used
    printf("3. text in buff is %s\n", buff);
    
}
```

The output is as follows:
```
1. text in buff is Kofi
2. text in buff is Kofi Mensah
3. text in buff is Surname is Mensah and first name is Kofi
```

