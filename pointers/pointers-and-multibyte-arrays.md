# Pointers and Multibyte Arrays

- Arrays do not always store simple values, and may be used to store more complex data, such as structs.
- These are known as multibyte-width structures.
- Continuing with the house analogy from [Pointers](./pointers.md), we could have a street, or an array of houses.

```c
typedef struct House {
    int SquareFeet;
    int NumBedrooms;
    int NumBathrooms;
} house_t;

house_t street[3] = {
    { 1000, 3, 1 },
    { 998, 3, 1 },
    { 800, 2, 1},
    }
```

- We can, of course access the data in the houses within `street` as normal:

```c
printf("House 1's square footage is %d\n", street[0].SquareFeet);
```

- But we can also use a pointer. The syntax is the same as before:

```c
house_t * pStreet = street;
printf("House 1's square footage is %d\n", (pStreet + 1)->SquareFeet)

// looping

for (int i = 0; i < 3; i++) {
    printf("House %d's square footage is %d\n", i+1, (pStreet + i)->SquareFeet);
};

// House 1's square footage is 1000
// House 2's square footage is 998
// House 3's square footage is 800
```
