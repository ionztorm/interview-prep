# Pointers

## TLDR

1. **What are pointers?**

   - Pointers are variables that stores the memory address of another variable as its value.
   - The pointer is said, therefore, to **point to** the variable whose memory address it holds.

2. **Defining Pointers**

   - Use `*` to indicate a variable is a pointer
   - Use `&` (_address of_ operator) to get the value/object memory address
   - `type * pVariable = &value`
   - The type of the pointer must match the type of the variable it points to.

3. **Dereferencing and Accessing Values**

   - Dereferencing allows you to access or modify the value stored at the memory address a pointer holds.

   - Simple Values:

     - Use \* before a pointer variable to access or modify the value.
     - Example: \*pValue = 10; — modifies the original value directly.

   - Objects:

     - Use the -> operator to automatically dereference and access members of an object.
     - Example: pObject->member (Equivalent to (\*pObject).member).

   - Without dereferencing, you are only working with the address, not the actual value.

4. **Pointer Efficiency**

   - Pointers are more efficient than regular values when passed as arguments to functions because they only require passing a memory address instead of copying entire objects.
   - The size of a pointer is always 4 bytes on a 32-bit system, and 8 bytes on a 64-bit system, regardless of the size of the data being pointed to.
   - This efficiency is especially noticeable when working with large objects or data structures, as only the memory address is passed instead of duplicating the entire data.

## House Analogy

1. Consider the analogy of a house.

   - In the real world if we want to invite people to our house, how do we let those people know where the house is? We may:
     - Go and get the people and drive them to the house to show each person where it is.
     - Create a copy of the house to show them what it looks like so they might recognise it.
     - Just give them the address.

2. The situation is not dissimilar in code.

   - In C, we may define the house in code as:

     ```c
     typedef struct {
         int SquareFeet;
         int NumBedrooms;
         int NumBathrooms;
     } House;
     ```

   - When we create a house object in code, either as a local or global variable, this object will be stored somewhere in memory.
     - All memory in the computer has an address, from byte 0 to the top.
     - The house object has 3 integer values; `SquareFeet`, `NumBedrooms`, and `NumBathrooms`.
     - Integers require 4 bytes of memory, meaning the house object needs 12 bytes in total.
     - The compiler finds a place in memory and puts the object there.
     - Typically, we have no idea where this has been stored.
     - Since we don't know the memory address, how do we share the address with other parts of our code (the people)? - a pointer.

3. A `pointer` is a _variable that stores, as its value, the memory address of another variable_.
   - It therefore, **points to** that variable and, as such, the type of the pointer must match the type of the variable it points to.

## Syntax (in C)

### Defining a Pointer

1. In C, we add a `*` in front of the variable name to indicate that it is a pointer.
2. Conventionally, we begin the pointer name with `p`.
3. We also define the type of the variable the pointer will point to.
4. To get the memory address of a variable, we preceed its name with `&`. This is the _address of_ operator.

```c
// define a house
House myHouse = { 1000, 3, 1 };

// initialise a pointer, pHouse that points to the memory address of someHouse.
House *pMyHouse;
pMyHouse = &myHouse;

// or we can do this on one line:
House *pMyHouse = &myHouse;
```

### Accessing values that are being pointed to.

1. Accessing the data being pointed to has a different syntax. In the case of the house object, we use `->` instead of the standard dot notation.
2. The arrow operator basically means:
   - Go to the object being pointed to
   - Then get get the member variable by name.

**Standard object acccess**

```c
myHouse.SquareFeet
myHouse.NumBedrooms
myHouse.NumBathrooms
```

**Pointer access**

```c
pMyHouse->SquareFeet
pMyHouse->NumBedrooms
pMyHouse->NumBathrooms
```

### Changing the value being pointed at

1. When you have a pointer to an object or a value, you can **modify the original data directly** by dereferencing the pointer.
   - This allows functions to update variables or objects without creating unnecessary copies.
2. Placing a `*` before a pointer variable allows you to access or modify the value at the memory address it points to.
   - This is different from using `*` when declaring a pointer, where it only indicates that the variable is a pointer.
3. Without dereferencing, you would only be working with the memory address itself, not the value it refers to.
   - Dereferencing is essential when you want to **change the original data** through a pointer.
4. In the house analogy, it's like someone having your house's address and **making changes directly to your house**, such as adding an extension, rather than creating a copy of your house and modifying that.

**Working with Objects (House Example)**

1. When working with pointers to objects, **dereferencing is not needed** when accessing or modifying members because the `->` operator **both dereferences the pointer and accesses the member variable** in one step.

```c
// Adds an extension to the house, increasing its square feet, bedrooms, and bathrooms
void AddExtension(House *pMyHouse, int additionalSquareFeet, int additionalBedrooms, int additionalBathrooms) {
    pMyHouse->SquareFeet += additionalSquareFeet;
    pMyHouse->NumBedrooms += additionalBedrooms;
    pMyHouse->NumBathrooms += additionalBathrooms;
}
```

**Working with Primitive Values (Integer Example)**

1. When working with pointers to simple data types like integers, you must **explicitly dereference the pointer** to access or modify the value.

```c
// Function to double a value using a pointer
void DoubleValue(int *pValue) {
    *pValue *= 2;
}
```

### Pointers and Functions

1. When defining a function, we can have that function accept a standard object, or we can have it accept a pointer.
2. Accepting a standard object is known as _pass by value_ and creates a copy of the object for use within the function scope.
3. Accpting a pointer is known as _pass by reference_ and allows the function to access the object directly.
4. Passing by reference is generally faster:

   - On a 32 bit system, a pointer is only 4 bytes, and on a 64 bit system, a pointer is 8 bytes, so that is all that is required to pass a pointer argument.
   - Passing by value requires as many bytes as the object itself. In the house example, this would be 12 bytes.
   - The difference is more noticeable the larger the object. Imagine an object with more properties; it's the memory required increases, while it does not for a pointer to it.

```c
// 12 byte argument - Copying the house (Pass by Value)
void InvitePeople(House myHouse) {
    printf("Inviting people to house at address: [COPY] %p\n", (void*)&myHouse);
    printf("Square Feet: %d, Bedrooms: %d, Bathrooms: %d\n",
           myHouse.SquareFeet, myHouse.NumBedrooms, myHouse.NumBathrooms);
}

// 4 or 8 byte argument - Providing the address (Pass by Reference)
void InvitePeople(House *pMyHouse) {
    printf("Inviting people to house at address: %p\n", (void*)pHouse);
    printf("Square Feet: %d, Bedrooms: %d, Bathrooms: %d\n",
           pMyHouse->SquareFeet, pMyHouse->NumBedrooms, pMyHouse->NumBathrooms);
}
// %p expects a void pointer. Covered later.
```
