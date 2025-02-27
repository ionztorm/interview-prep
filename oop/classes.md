# Classes

## What is a class

A class is a blueprint for creating objects. It defines the properties and methods that an object will have.

We can create instances of a class, which are objects that are created based on the class definition.

This allows us to create multiple instances of the same class, each with its own properties and methods.

Classes may contain properties, which are variables that store data, and methods, which are functions that perform actions.

## What is a method

A method is a function that is defined inside a class. It can access the properties of the object using the `self` keyword.

## The self keyword

The `self` keyword is used to refer to the current instance of the class. It is used to access the properties and methods of the object.

When defining a method in a class, the first parameter should be `self`, which is a reference to the object itself.

```python
def full_name(self):
    return f"{self.first_name} {self.last_name}"
```

This method uses the `self` keyword to access the `first_name` and `last_name` properties of an instance of a class.

## Defining a class in Python

To define a class in Python, we use the `class` keyword followed by the class name. The class definition can contain properties and methods.

```python
class MyClass:
    first_name = "Leon"
    last_name = "Lonsdale"

    def full_name(self):
        return f"{self.first_name} {self.last_name}"

```

This defines a class called `MyClass` with a property called `name` that has the value `"Leon"`. It also defines a method called `full_name` that returns the full name of the person.

### The **init** method

The `__init__` method is a special method that is called when an instance of a class is created. It is used to initialize the properties of the object.

```python
class Person:
    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

### Variables : Instance and Class Variables

Instance variables are variables that are unique to each instance of a class. They are defined inside the `__init__` method and are accessed using the `self` keyword.

Class variables are variables that are shared by all instances of a class. They are defined outside of any method and are accessed using the class name.

```python
class Person
    species = "human" # class variable

    def __init__(self, first_name, last_name):
        self.first_name = first_name # instance variable
        self.last_name = last_name # instance variable

    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

### Private Variables

In Python, variables can be made private by prefixing them with two underscores (`_`). This does not make them inaccessible from outside the class unfortunitely, but it is convention, and indicates to other developers that they should not use it.

```python
class Person:
    species = "human" # class variable

    def __init__(self, first_name, last_name):
        self.__first_name = first_name # private instance variable
        self.__last_name = last_name # private instance variable

    def full_name(self):
        return f"{self.__first_name} {self.__last_name}"
```

## Creating an instance of a class

To create an instance of a class, we use the class name followed by parentheses. We can then access the properties and methods of the object using the dot notation.

```python
leon = Person("Leon", "Lonsdale")
leon.full_name() # "Leon Lonsdale"
```

## Class Methods

Class methods are methods that are bound to the class itself, rather than to an instance of the class. They are defined using the `@classmethod` decorator.

```python
class Person:
    species = "human" # class variable

    def __init__(self, first_name, last_name):
        self.first_name = first_name # instance variable
        self.last_name = last_name # instance variable

    def full_name(self):
        return f"{self.first_name} {self.last_name}"

    @classmethod
    def from_full_name(cls, full_name):
        first_name, last_name = full_name.split(" ")
        return cls(first_name, last_name)
```

Class methods are used when a method needs access to the class itself, rather than to an instance of the class.

```python
leon = Person.from_full_name("Leon Lonsdale")
leon.full_name() # "Leon Lonsdale"
```

## Static Methods

Static methods are methods that are not bound to the class or an instance of the class. They are defined using the `@staticmethod` decorator.

```python
class Person:
    species = "human" # class variable

    def __init__(self, first_name, last_name):
        self.first_name = first_name # instance variable
        self.last_name = last_name # instance variable

    def full_name(self):
        return f"{self.first_name} {self.last_name}"

    @classmethod
    def from_full_name(cls, full_name):
        first_name, last_name = full_name.split(" ")
        return cls(first_name, last_name)

    @staticmethod
    def is_adult(age):
        return age >= 18
```

They are used when a method does not need access to the class or instance, and can be called without creating an instance of the class.

```python
Person.is_adult(21) # True
```

## Property Decorators

Property decorators are used to define properties in a class that behave like attributes, but are computed dynamically.

```python
class Person:
    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

## Inheritance

Inheritance is a way to create a new class that inherits the properties and methods of an existing class. The new class is called a subclass, and the existing class is called a superclass.

```python
class Student(Person):
    def __init__(self, first_name, last_name, student_id):
        super().__init__(first_name, last_name)
        self.student_id = student_id
```

## Classes as Class Variables

Class variables and private variables can be used to store instances of other classes.

```python
class Address:
    def __init__(self, street, city, state, zip_code):
        self.street = street
        self.city = city
        self.state = state
        self.zip_code = zip_code

class Person:
    def __init__(self, first_name, last_name, address):
        self.first_name = first_name
        self.last_name = last_name
        self.address = Address(**address)

## ** unpacks the dictionary into keyword arguments. So, if you have a dictionary like this:
## address = {'street': '123 Main St', 'city': 'Springfield', 'state': 'IL', 'zip_code': '62701'}
## You can pass it to the Address constructor like this:
## address = Address(**address)
```

We can access a person's address and address properties like this:

```python
address = {
    'street': '123 Main St',
    'city': 'Springfield',
    'state': 'IL',
    'zip_code': '62701'
}

leon = Person("Leon", "Lonsdale", address)
leon.address.city # "Springfield"

# If accessing the address properties within the person class, you can use the self keyword:
class Person:
    def __init__(self, first_name, last_name, address):
        self.first_name = first_name
        self.last_name = last_name
        self.address = Address(**address)

    def full_address(self):
        return f"{self.address.street}, {self.address.city}, {self.address.state} {self.address.zip_code}"
```
