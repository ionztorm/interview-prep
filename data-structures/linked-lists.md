# Linked lists

A linked list is a linear, odered data structure made up of nodes.

Each node contains a value and a reference to the next node in the sequence.

Linked lists can be singly or doubly linked. In a doubly linked list, each node
also contains a reference to the previous node.

```python
from typing import Generic, TypeVar

T = TypeVar('T')

class Node(Generic[T]):
    def __init__(self, value: T, next: Node[T] = None):
        self.value = value
        self.next = next

    def set_next(self, next: Node[T]):
        self.next = next

    def __repr__(self) -> T:
        return self.value


class LinkedList(Generic[T]):

    def __init__(self, head: Node[T] = None):
        self.head: Node[T] | None = head
        self.tail: Node[T] | None = None

    def __iter__(self) -> Node[T]:
        current_node = self.head
        while current_node:
            yield current_node
            current_node = current_node.next
    
    @override
    def __repr__(self) -> str:
        nodes = [str(node.value) for node in self]
        return " -> ".join(nodes) if nodes else "Empty List"

    def add_at_head(self, value: T) -> None:
        node = Node(value)

        if not self.head:
            self.head = self.tail = node
            return

        node.set_next(self.head)
        self.head = node

    def remove_at_head(self) -> Node[T] | None:
        if not self.head:
            return None

        removed = self.head
        self.head = self.head.next

        if not self.head:
            self.tail = None

        return removed 

    def add_at_tail(self, value: T) -> None:
        node = Node(value)

        if self.tail:
            self.tail.set_next(node)
        else:
            self.head = node

        self.tail = node
```
