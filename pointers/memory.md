
# A Basic Overview of Memory

## Bits, Bytes, and Addresses

1. Memory can be thought of as a collection of boxes where:
   - Each box is a **byte**.
   - Each byte has a unique **address**.
   - A byte contains **8 bits** (binary digits: `0` or `1`).
   - 4 bits is called a `nibble`.

2. **Addresses:**
   - Memory addresses are represented in **hexadecimal format** (base-16).
   - Example: `0x7ffee6bdc8`.

## Storing Data in Memory

When a program is compiled, the **compiler allocates memory** for variables based on their **data type**. This process involves:

- Reserving a specific number of bytes in memory depending on the data type.
- Associating a memory address with the variable.
- Ensuring that the memory allocated is contiguous if the variable is part of an array.

The number of bytes used for each type is consistent across arrays, pointers, and all other memory operations.

### Data Types and Their Sizes

| Data Type | Size (Bytes) |
|-----------|--------------|
| `char`    | 1             |
| `short`   | 2             |
| `int`     | 4             |
| `long`    | 8             |
| `float`   | 4             |
| `double`  | 8             |

Understanding how much memory is allocated to each data type is essential for correctly working with pointers and arrays.

## Memory Offsets for Arrays

When arrays are stored in memory, each element is placed in consecutive memory locations. The address of each element is calculated based on the data type size.

### Example: Integer Array (`int`)

```c
int arr[4] = {10, 20, 30, 40};
```

| Element | Address (Hex)      | Memory Offset |
|---------|---------------------|---------------|
| arr[0]  | 0x7ffee6bd99c8      | +0            |
| arr[1]  | 0x7ffee6bd99cc      | +4            |
| arr[2]  | 0x7ffee6bd99d0      | +8            |
| arr[3]  | 0x7ffee6bd99d4      | +12           |

### Example: Float Array (`float`)

```c
float arr[4] = {1.0, 2.0, 3.0, 4.0};
```

| Element | Address (Hex)      | Memory Offset |
|---------|---------------------|---------------|
| arr[0]  | 0x7ffee6bd99c8      | +0            |
| arr[1]  | 0x7ffee6bd99cc      | +4            |
| arr[2]  | 0x7ffee6bd99d0      | +8            |
| arr[3]  | 0x7ffee6bd99d4      | +12           |

### Example: Long Array (`long`)

```c
long arr[4] = {1000, 2000, 3000, 4000};
```

| Element | Address (Hex)      | Memory Offset |
|---------|---------------------|---------------|
| arr[0]  | 0x7ffee6bd99c8      | +0            |
| arr[1]  | 0x7ffee6bd99d0      | +8            |
| arr[2]  | 0x7ffee6bd99d8      | +16           |
| arr[3]  | 0x7ffee6bd99e0      | +24           |
