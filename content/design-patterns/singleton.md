---
title: "Singleton with examples in Python"
date: 2023-05-16T21:40:50+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/singleton.png
    alt: "singleton"
tags: ["design-patterns"]
---

Singleton design pattern is a type of creational pattern which we use when we need to provide global access to an object. Basically, a class will only have one object.

Let's understand the above with an example:
```python
class Singleton(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Car(metaclass=Singleton):
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year

car1 = Car("Company1", "Car1", 2023)
car2 = Car("Company2", "Car2", 2023)

print(car1 is car2)
```
Output:
```text
True
```

Here, `Singleton` is a metaclass that ensures that we only ever create one instance of `Car`. When we call `Car()` to create an instance, the call method of the metaclass is invoked. If an instance of `Car` doesn't exist, it creates one and stores it in `_instances`. If it already exists, it returns the existing one.

Practical applications of Singleton design pattern includes creating object for logging, DB connection, shared resources (e.g. class having a counter), etc. This helps us ensure consistency.

Hope the post have created some value. Peace!