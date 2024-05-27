---
title: "Decorator with examples in Python"
date: 2024-02-03T20:25:19+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/decorator.png
    alt: "decorator"
tags: ["design-patterns"]
---

The decorator pattern is a design pattern in programming that allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class.

In real world, imagine we are decorating a plain Christmas tree. We start with a simple tree, and we add decorations to it such as lights, ornaments, and tinsel. Each decoration enhances the tree by adding a layer of detail without changing its structure. We can add or remove decorations freely without affecting the underlying tree.

Similarly, in programming, the decorator pattern is used to "decorate" objects with additional features or behaviors without changing the object's class. Each decorator adds some functionality, wrapping the original object, just like ornaments wrapping the tree.

Let's understand this with an example:
```python
class Car:
    def __init__(self):
        self._description = "Basic Car"

    def get_description(self):
        return self._description

    def get_cost(self):
        # Cost of the basic car
        return 10000
```
Now, let's define some decorators to add features to the car:

```python
class PremiumPackageDecorator:
    def __init__(self, car):
        self._car = car

    def get_description(self):
        return self._car.get_description() + ", with premium package"

    def get_cost(self):
        return self._car.get_cost() + 5000

class SportsPackageDecorator:
    def __init__(self, car):
        self._car = car

    def get_description(self):
        return self._car.get_description() + ", with sports package"

    def get_cost(self):
        return self._car.get_cost() + 7000
```

```python
# Create a basic car
my_car = Car()
print(my_car.get_description())
print(my_car.get_cost())

# Add premium package
my_car = PremiumPackageDecorator(my_car)
print(my_car.get_description())
print(my_car.get_cost())

# Add sports package
my_car = SportsPackageDecorator(my_car)
print(my_car.get_description())
print(my_car.get_cost())
```

Output:
```text
Basic Car
10000
Basic Car, with premium package
15000
Basic Car, with premium package, with sports package
22000
```

In python we have "@" decorators that we can use on functions.
```python
def basic_car_description():
    """A simple function that returns a basic car's description."""
    return "Basic Car"

def basic_car_cost():
    """A simple function that returns a basic car's cost."""
    return 10000

def premium_package(func):
    """Decorator function to add premium package features to a car's description."""
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) + ", with premium package"
    return wrapper

def sports_package(func):
    """Decorator function to add sports package features to a car's description."""
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) + ", with sports package"
    return wrapper

def additional_cost(amount):
    """Decorator function to add additional cost to a car."""
    def decorator(func):
        def wrapper(*args, **kwargs):
            return func(*args, **kwargs) + amount
        return wrapper
    return decorator

# Decorating the functions
@premium_package
def get_premium_car_description():
    return basic_car_description()

@additional_cost(5000)
def get_premium_car_cost():
    return basic_car_cost()

@premium_package
@sports_package
def get_sports_premium_car_description():
    return basic_car_description()

@additional_cost(12000)
def get_sports_premium_car_cost():
    return basic_car_cost()

print(get_premium_car_description())
print(get_premium_car_cost())
print(get_sports_premium_car_description())
print(get_sports_premium_car_cost())
```

Output:
```text
Basic Car, with premium package
15000
Basic Car, with sports package, with premium package
22000
```