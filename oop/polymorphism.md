# Polymorphism

- [Follow on Bluesky](https://bsky.app/profile/leonlonsdale.dev)
- [Join Discord](https://discord.gg/dhrdFh98UA)

- Polymorphism is the ability of a variable, function, or object to take on multiple forms.
- In OOP, it is the ability for classes in the same hierarchy to have different implementations of the same method (the method has the same name).

There are two main types of polymorphism in object-oriented programming:

- Compile-time polymorphism is achieved through method overloading and operator overloading.
- Runtime polymorphism is achieved through method overriding and virtual functions.

The differences:

- Method overriding is when a subclass provides a specific implementation of (overrides) a method that is already defined in its parent class.
- Method overloading is when a class has multiple methods with the same name but `different parameters` (number or type of, or order of parameters).

## Example of Method Overriding

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print("Woof!")

class Cat(Animal):
    def speak(self):
        print("Meow!")
```

- In the example above, we have a parent class `Animal` with a method `speak` that is overridden by the child classes `Dog` and `Cat`. When you call the `speak` method on an object of type `Dog`, it will print "Woof!", and when you call it on an object of type `Cat`, it will print "Meow!".
- In python we use the keyword `pass` to indicate that the method is empty and will be overridden by the child classes.

## Example Method Overloading and Operator Overloading

Method overloading is a feature that allows a class to have multiple methods with the same name but different parameters. This is useful when you want to provide different ways to call a method based on the arguments passed to it.

Operator overloading is a feature that allows a class to define how an operator should behave when applied to objects of that class. This is useful when you want to provide custom behavior for operators such as `+`, `-`, `*`, `/`, etc.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2
print(p3.x, p3.y) # Output: 4 6
```

- In the example above, we have defined a class `Point` with an `__add__` method that allows us to add two `Point` objects together using the `+` operator. When we add two `Point` objects `p1` and `p2`, the `__add__` method is called and returns a new `Point` object `p3` with the sum of the `x` and `y` coordinates of `p1` and `p2`.
- The `__add__` method is an example of operator overloading, where we define custom behavior for the `+` operator when applied to `Point` objects.
