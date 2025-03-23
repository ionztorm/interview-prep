# Pointers and Strings

## Introduction

- In C, **strings** are represented as arrays of characters terminated by a null character `\0`.
- Pointers are frequently used with strings, as they allow direct manipulation and traversal of these character arrays.
- Understanding how pointers interact with strings is essential for efficient string manipulation and memory management.

## Declaring and Initialising Strings

- Strings can be declared and initialised using arrays or pointers.

### Using Character Arrays

```c
char str1[] = "Hello"; // Stored in stack memory, mutable
```

- This creates an array of size 6 (`'H'`, `'e'`, `'l'`, `'l'`, `'o'`, `\0`).

#### Memory Layout

| 0x1000 | 0x1001 | 0x1002 | 0x1003 | 0x1004 | 0x1005 |
| ------ | ------ | ------ | ------ | ------ | ------ |
| H      | e      | l      | l      | o      | \0     |

### Using Pointers

```c
char *str2 = "World"; // Stored in read-only memory, immutable
```

- This points to a string literal, which should not be modified.

#### Memory Layout

| 0x2000 | 0x2001 | 0x2002 | 0x2003 | 0x2004 | 0x2005 |
| ------ | ------ | ------ | ------ | ------ | ------ |
| W      | o      | r      | l      | d      | \0     |

## Pointer Arithmetic with Strings

- Pointers can be incremented or decremented to traverse through strings.
- Example:

```c
char *str = "Pointers";
while (*str != '\0') {
    printf("%c\n", *str);
    str++;
}
```

- This prints each character of the string on a new line by incrementing the pointer.

## Passing Strings to Functions

- Functions often accept pointers to strings for efficiency.
- Example:

```c
void printString(char *str) {
    while (*str != '\0') {
        printf("%c", *str++);
    }
}
```

## Comparing Strings

- Strings cannot be compared using the `==` operator because it compares memory addresses.
- Instead, functions like `strcmp()` are used:

```c
#include <string.h>
if (strcmp(str1, str2) == 0) {
    printf("The strings are equal.\n");
}
```

## Modifying Strings

- When using pointers, be careful with modifying strings stored in read-only memory.
- Example of **mutable string**:

```c
char str[] = "Mutable";
str[0] = 'M'; // This is valid
```

## Common Pitfalls

- Attempting to modify string literals:

```c
char *str = "Hello";
str[0] = 'h'; // Causes a segmentation fault
```

- Always ensure pointers are properly initialised before dereferencing.

## Example: Creating a string concatenation function.

```c
void concat_strings(char *str1, const char *str2) {
    char *last = str1; // avoid mutating str1 incase needed later.

    // iterate over string to find '\0' null terminator.
    while (*last != '\0') {
        last++;
    }

    // copy str2 chars to the end of str1
    while (*str2 != '\0') {
        *last = *str2;
        last++;
        str2++;
    }

    // add null terminator to the end
    *last = '\0';
}
```
