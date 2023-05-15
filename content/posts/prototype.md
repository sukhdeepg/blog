---
title: "Prototype"
date: 2023-05-12T14:33:06+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/prototype.png
    alt: "prototype"
tags: ["fundamentals", "low-level-design", "design patterns"]
---

The Prototype Design Pattern is a creational design pattern that involves duplicating or "cloning" existing objects to create new ones, rather than creating new objects from scratch. This is useful when object creation is time-consuming or complex. This means, instead of creating a new object and setting it up, we make a copy of an existing object and modify it as needed.

Let's understand the above with an example:
```python
import copy

class Car:
    def __init__(self, model, color, engine):
        self.model = model
        self.color = color
        self.engine = engine

    def clone(self):
        return copy.deepcopy(self)

    def __str__(self):
        return f'{self.color} {self.model} with a {self.engine} engine'


if __name__ == "__main__":
    car1 = Car('car1', 'red', 'electric')
    print(car1)

    car2 = car1.clone()
    car2.model = 'car2'
    car2.color = 'blue'
    print(car2)
```

Output:
```text
red car1 with a electric engine
blue car2 with a electric engine
```

In the above example, we first create a `Car` object from scratch, i.e., car1 has a red color and electric engine. Now, we need a similar `Car` object that has a different model and color. So, instead of creating the car2 object from scratch, we just make a copy of the car1 object and make the modifications. In this case, car1 is the prototype for car2.

> But, why do we need to clone an object? we can always create a new object right?

In most cases, creating a new object is the straightforward approach. However, Prototype pattern is useful when creating a new object is resource-intensive, such as when it requires a significant amount of computation, disk reads, network calls, etc. Also when we have an object in a certain state and we need another object just like it.

Hope the post have created some value. Peace!