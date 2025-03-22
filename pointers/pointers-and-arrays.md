# Pointers and Arrays

> Note: Examples and syntax used in this documen use C.

## Arrays Revision

- We can define an array as follows:

  ```c
  int myArray[5] = { 1, 2, 3 ,4 ,5 };
  ```

- This creates:

  - An `int`eger array of length 5.
  - Each integer in the array requires `4 bytes` of memory.
  - The array requires a total of `20 bytes` (5 x 4 = 20).

- We can iterate over the array with a for loop:

  ```c
  for (int i = 0; i < 5; i++) {
      printf("The integer at index %d is %d\n", i, myArray[i]);
  }
  /*
  The integer at index 0 is 1
  The integer at index 1 is 2
  The integer at index 2 is 3
  The integer at index 3 is 4
  The integer at index 4 is 5
  */
  ```

- We can print the memory address of each integer using the `address at` operator, `&`:

  ```c
  for (int i = 0; i < 5; i++) {
      printf("The integer at index %d is %d. Its address is %p\n", i, myArray[i], &myArray[i]);
  }
  /*
  The integer at index 0 is 1. Its address is 0x98989f0
  The integer at index 1 is 2. Its address is 0x98989f4
  The integer at index 2 is 3. Its address is 0x98989f8
  The integer at index 3 is 4. Its address is 0x98989fC
  The integer at index 4 is 5. Its address is 0x98989f4
  */
  ```

- Notice that the last digit of the address increases by 4. This is because an integer is 4 bytes.
- The compiler knows this, and reserves 4 bytes for each integer in the array.

## Array Pointers

### Array Names and Creating Pointers to them

- The name of an array (`myArray`) is effectively a pointer to its first element.
- If we print the array name using `%p`, the output is the memory address of the first array element.

  ```c
  printf("%p\n", myArray); // 0x98989f0
  printf("%p\n", &myArray[0]); // 0x98989f0
  ```

- This is because the array name `decays to a pointer` to the first element when used in expressions.

> In C, when using an array name in an expression, it automatically converts to a pointer to the first element of the array. This is known as decaying. Technically this means the array name is not actually a pointer, but the compiler treats it as such. This is true when:
>
> - Passing the array to a function.
> - Assigning the array to a pointer.
> - Performing pointer arithmetic.
>
> It does not decay when:
>
> - Using `sizeof`.
> - When using `&`.
>
> ```c
> printf("Size of myArray: %zu\n", sizeof(myArray)); // Outputs 20
> printf("Size of pMyArray: %zu\n", sizeof(pMyArray)); // Outputs 8 (on 64-bit systems)
> ```

- We can also explicitly create a pointer to the first element of an array.

  ```c
  // no & needed as myArray already points to an address
  int * pMyArray = myArray;
  printf("%p\n", pMyArray); // 0x98989f0
  ```

- Both `myArray` and `pMyArray` behave the same, and both can be used with `pointer arithmetic` to access or update array elements.

### Pointer Arithmetic and Accessing Array Elements

- Since Pointers are just memory addresses, `pointer arithmetic` allows us to navigate memory based on the size of the data type we are dealing with.
- Moving a pointer by one position (ptr + 1) moves it by 1 x the size of the data type.
  - For `int` types, `ptr + 1` moves the pointer 4 bytes forward.

1. Memory allocation for an array is contiguous; `elements are stored in bytes next to each other in memory.`

```c
int * pMyArray = myArray;
printf("%d\n", *pMyArray); // 1
printf("%d\n", *(pMyArray + 1)); // 2
printf("%d\n", *(pMyArray + 4)); // 5

// Similarly...
printf("%d\n", *myArray); // 1
printf("%d\n", *(myArray + 1)); // 2
printf("%d\n", *(myArray + 4)); // 5
```

- The compiler calculates the address by:
  - `First address + (index * size of each element in bytes)`
- In the example array, that is:

  - `First address + (index * 4)`

- **Pointer arithmetic is powerful but must be used carefully to avoid memory access errors. This can occur if you attempt to access memory beyond the array's bounds, potentially leading to unexpected behavior, crashes, or security vulnerabilities.**

### Updating Array Elements Using Pointers

- Modifying array elements using pointers:

  ```c
  int myArray[5] = { 1, 2, 3 ,4 ,5 };

  // update the first element
  *myArray *= 2;

  // update the last element
  *(myArray + 4) *= 2;

  // myArray is now { 2, 2, 3, 4, 10 }
  ```
