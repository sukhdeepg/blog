---
title: "Composite with examples in Python"
date: 2023-06-13T20:28:09+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/composite.png
    alt: "composite"
tags: ["design-patterns"]
---

The Composite Design Pattern is a structural design pattern that lets us compose objects into tree structures to represent part-whole hierarchies.
To expand this further:
This pattern is all about creating objects that have other objects inside them. Let's break down the last sentence further:

1. **Compose objects into tree structures**: This means that we're making some objects that contain other objects. This is similar to how a family tree works: a parent can have children, and those children can also be parents to their own children. In computer science, this is referred to as a "tree" structure.

2. **To represent part-whole hierarchies**: This means that the objects that are inside other objects are considered part of the larger object. It's a way to represent a hierarchy or relationship between things. Like in a car, an engine, wheels, and a body are parts of the car as a whole. The car is the "whole", and the engine, wheels, and body are the "parts".

So in simple terms, the Composite Design Pattern is a way to make complex objects that are made up of other smaller objects, and this pattern allows us to organize these objects in a way that represents a hierarchy or relationship between them.

Let's understand this with an example:
```python
from abc import ABC, abstractmethod
from typing import List

class CarComponent(ABC):
    @abstractmethod
    def operation(self) -> str:
        pass

class LeafElement(CarComponent):
    def __init__(self, name):
        self.name = name

    def operation(self) -> str:
        return self.name


class Composite(CarComponent):
    def __init__(self, name) -> None:
        self.name = name
        self._children: List[CarComponent] = []

    def add(self, component: CarComponent) -> None:
        self._children.append(component)

    def remove(self, component: CarComponent) -> None:
        self._children.remove(component)

    def operation(self) -> str:
        results = []
        for child in self._children:
            results.append(child.operation())
        return f"{self.name}: {', '.join(results)}"


if __name__ == "__main__":
    # simple components
    engine = LeafElement("Engine")
    wheel1 = LeafElement("Wheel1")
    wheel2 = LeafElement("Wheel2")
    wheel3 = LeafElement("Wheel3")
    wheel4 = LeafElement("Wheel4")

    # complex components (composite)
    wheels = Composite("Wheels")
    car = Composite("Car")

    # tree structure
    wheels.add(wheel1)
    wheels.add(wheel2)
    wheels.add(wheel3)
    wheels.add(wheel4)

    car.add(engine)
    car.add(wheels)

    print(car.operation())
```

Output:
```text
Car: Engine, Wheels: Wheel1, Wheel2, Wheel3, Wheel4
```

Some real world scenarios where this design pattern can be used:
1. **File Systems**: A file system is a classic example of a Composite pattern. A directory can contain files or other directories. Here, 'Directory' is a Composite, and 'File' is a Leaf.
2. **GUI Widgets**: In graphical applications, a container widget (like a window or a panel) can contain other widgets (like buttons and checkboxes) or even other containers. This is another case where the Composite pattern is useful.

Hope the post have created some value. Peace!