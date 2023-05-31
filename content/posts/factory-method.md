---
title: "Factory Method with examples in Python"
date: 2023-05-01T11:10:03+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/factory_method.png
    alt: "factory_method"
tags: ["fundamentals", "low-level-design", "design patterns"]
---

The Factory Method is a creational design pattern which is great for managing object creation in a clean, modular, and scalable way. It promotes loose coupling and code reusability. This pattern comes handy when we have multiple object types with a shared interface or base class, and we want to create new objects based on a given parameter without hardcoding the exact classes.

What exactly does factory mean?
"Factory" refers to an object that is responsible for creating another object. In real world factories, we input raw materials and design specfication and we get goods as an output. Here, we input a type or a set of parameters and we get an object as an output.
<br/>

Let's understand the above with an example:
```python
from abc import ABC
from abc import abstractmethod

class Car(ABC):
    @abstractmethod
    def start(self):
        pass


class ElectricCar(Car):
    def start(self):
        return "Starting electric car!"


class GasolineCar(Car):
    def start(self):
        return "Starting gasoline car!"


class HybridCar(Car):
    def start(self):
        return "Starting hybrid car!"
```
Here, the `ElectricCar`, `GasolineCar`, and `HybridCar`, extends the `Car` abstract base class. This means the `start` method needs to be implemented.
<br/>

Now, we'll create `Car Factory`.
```python
class CarFactory:
    def __init__(self):
        self._car_map = {}

    def create_car(self, car_type):
        car_class = self._car_map.get(car_type)
        if car_class:
            return car_class()
        else:
            raise ValueError(f"Invalid car type: {car_type}")

    def register_car(self, car_type, car_class):
        self._car_map[car_type] = car_class
```
Now, we can create car objects based on the `car_type` parameter without hardcoding the exact classes.
<br/>

```python
def main():
    car_factory = CarFactory()

    car_factory.register_car("electric", ElectricCar)
    car_factory.register_car("gasoline", GasolineCar)
    car_factory.register_car("hybrid", HybridCar)

    electric_car = car_factory.create_car("electric")
    print(electric_car.start())

    gasoline_car = car_factory.create_car("gasoline")
    print(gasoline_car.start())

    hybrid_car = car_factory.create_car("hybrid")
    print(hybrid_car.start())

if __name__ == "__main__":
    main()
```

The output:
```text
Starting electric car!
Starting gasoline car!
Starting hybrid car!
```
<br/>

Now, the above has few benefits:
1. Decoupling: `CarFactory` decouples the creation of car objects from their usage. Client doesn't need to know about the concrete car classes (`ElectricCar`, `GasolineCar`, and `HybridCar`). This helps make code more modular and easy to maintain.
2. Extensibility: If we need to add a new car type, we can simply create a new class for the car type, extend `Car` abstract base class, and register the car type with `CarFactory`. This helps adding new car types without affecting the existing code. 

Hope the post have created some value. Peace!