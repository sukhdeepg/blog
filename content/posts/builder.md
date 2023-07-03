---
title: "Builder with examples in Python"
date: 2023-05-08T23:06:55+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/builder.png
    alt: "builder"
tags: ["design-patterns"]
---

The Builder design pattern is a method for constructing complex objects step-by-step, allowing you to create different configurations or variations of the object without altering the main class representing the object. It simplifies object creation by providing a clear and flexible way to build objects with multiple options or components.

Let's understand the above with an example:
```python
class CarBuilder:
    def __init__(self):
        self.car = Car()

    def set_wheels(self, wheels):
        self.car.wheels = wheels
        return self

    def set_color(self, color):
        self.car.color = color
        return self

    def set_seats(self, seats):
        self.car.seats = seats
        return self

    def build(self):
        return self.car

class Car:
    def __init__(self):
        self.wheels = None
        self.color = None
        self.seats = None

    def __str__(self):
        return f"Car with {self.wheels} wheels, {self.color} color, and {self.seats} seats."

builder = CarBuilder()
builder.set_wheels(4)
builder.set_color("blue")
builder.set_seats(4)
car = builder.build()

print(car)
```

The output:
```text
Car with 4 wheels, blue color, and 4 seats.
```

Here, `CarBuilder` is responsible for building the `Car` object. It will set the number of wheels, color and number of seats. The `build` method will return the final object.

But, why do we need the `CarBuilder` here? We can just put all of this in the `Car` class itself.
The builder pattern becomes useful in cases where the `Car` class has many optional or complex configurations. So, instead of creating multiple subclasses or sending multiple variables in the constructor, the `CarBuilder` way is more easy to read and maintain.

Hope the post have created some value. Peace!