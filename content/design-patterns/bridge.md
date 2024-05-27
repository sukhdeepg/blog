---
title: "Bridge with examples in Python"
date: 2023-06-06T22:26:39+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/bridge.png
    alt: "bridge"
tags: ["design-patterns"]
---

The Bridge Design Pattern is a structural design pattern that aims to separate what a system does from how it does it, so we can change the 'what' and the 'how' independently.

In other words, it organizes code in a way that lets us modify the operations a system can perform (like starting a car engine), and the details of how those operations are performed (like whether it's a petrol or electric engine), separately. This makes the code easier to update and manage.

It's helpful when we have a monolithic class and we want to divide it further to simplify maintenance.

Imagine that there are two dimensions: "car type" and "car engine type". If we want to create classes for every possible combination, there will be quite a few (sedan with petrol engine, sedan with electric engine, SUV with petrol engine, SUV with electric engine, etc.). Instead, we can separate these two dimensions into different class hierarchies, and then combine them - effectively "building a bridge" between "car type" and "car engine type".

Let's understand this with an example:
```python
from abc import ABC, abstractmethod

class Engine(ABC):
    @abstractmethod
    def start_engine(self):
        pass

class PetrolEngine(Engine):
    def start_engine(self):
        return "Starting the petrol engine"

class ElectricEngine(Engine):
    def start_engine(self):
        return "Starting the electric engine"

class Car(ABC):
    def __init__(self, engine: Engine):
        self._engine = engine

    @abstractmethod
    def start_car(self):
        pass

class Sedan(Car):
    def start_car(self):
        return f"Sedan: {self._engine.start_engine()}"

class SUV(Car):
    def start_car(self):
        return f"SUV: {self._engine.start_engine()}"

sedan_with_petrol_engine = Sedan(PetrolEngine())
suv_with_electric_engine = SUV(ElectricEngine())

print(sedan_with_petrol_engine.start_car())
print(suv_with_electric_engine.start_car())
```

Output:
```text
Sedan: Starting the petrol engine
SUV: Starting the electric engine
```

In this code, `Car` and `Engine` are the two dimensions. `Car` is the 'abstraction' and `Engine` is the 'implementation'. This way, adding a new car type or a new engine type does not affect each other.

The Bridge Design Pattern is handy in many scenarios where we want to keep the high-level operations in a system separate from the low-level details. This pattern is used in GUI systems to support multiple operating systems, in software to communicate using different protocols with hardware devices, in database interactions to support various types of databases, and in media players to decode different file formats. Essentially, the Bridge pattern is about segregating "what" a system does from "how" it does it, allowing both to evolve independently.

Hope the post have created some value. Peace!