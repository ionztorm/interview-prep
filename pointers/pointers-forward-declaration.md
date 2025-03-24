# Forward Declaration

On some occasions, we may need a struct that references itself, or be used recursively.

An example would be a `Node` in a binary tree or linked list.

```c
typedef struct Node {
    int value;
    node_t *next;
} node_t;
```

We can use forward declaration to solve this:

```c
typedef struct Node node_t;

typedef struct Node {
    int value;
    node_t *next;
} node_t;
```

The forward declaration must match. In this example, `Node`.

For example, this will not work:

```c
typedef struct Node node_t;

typedef struct SomeOtherName {
    int value;
    node_t *next;
} node_t;
```

## Mutual Structs

Forward declaration is also used when multiple structs need to reference eachother.

```c
typedef struct Employee employee_t;
typedef struct Department department_t;

typedef struct Employee {
    int id;
    char *name;
    department_t *department;
} employee_t;

typedef struct Department {
    char *name;
    employee_t *manager;
} department_t;
```

### Why We Use Pointers (Important!)

> In the example, we reference `manager` and `department` with pointers because:
>
> - **Department (`department_t *department` in `Employee`)**: Many employees can belong to a single department. Passing by value creates a copy of the department. If any changes are made to a department (like renaming it), we want this to be reflected for all employees that are part of it.
> - **Employee (`employee_t *manager` in `Department`)**: The same idea applies here. If the `Employee` struct changes (like the manager changing their name), we want this change to be reflected in the `Department` that references them. If we passed by value instead of by pointer, the original `Employee` would be updated, but the copy in the `Department` would not.
> - **Additionally, Circular Dependency Prevention:** Since the `Department` struct references an `Employee` and the `Employee` struct references a `Department`, passing by value would create infinite nesting; `Department` contains `Employee` which contains `Department` which contains `Employee`... Using pointers breaks this dependency loop.

### Why This Matters:

Forward declaration is crucial when creating complex data structures where multiple structs reference each other. By using pointers and forward declarations, we ensure our code is flexible, maintainable, and avoids circular dependency issues. This pattern is commonly seen in linked lists, trees, graphs, and many interdependent structures in C.

### Common Pitfalls:

- **Forgetting to Use Pointers:** If you mistakenly define `employee_t manager;` instead of `employee_t *manager;`, you will end up copying the entire struct, which is inefficient and breaks the purpose of dynamic referencing.
- **Dereferencing Null Pointers:** Always ensure pointers are properly initialised. Attempting to access or modify data via a null pointer will result in segmentation faults.
- **Mismatch in Forward Declaration:** The type name in the forward declaration must match exactly. Using different names will cause compilation errors.
