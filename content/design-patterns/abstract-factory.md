---
title: "Abstract Factory with examples in Python"
date: 2023-05-07T14:44:52+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/abstract_factory.png
    alt: "abstract_factory"
tags: ["design-patterns"]
---

Abstract Factory is a creational design pattern that helps create groups of related objects without knowing their specific classes. It's particularly useful when we need to create objects that belong to a family, but we don't care about the specific implementation.

First, let's understand <mark>create groups of related objects without knowing their specific classes</mark> with a small example:
```python
class ShapeFactory:
    def create_shape(self, shape_type):
        if shape_type == 'circle':
            return Circle()
        elif shape_type == 'square':
            return Square()
        elif shape_type == 'triangle':
            return Triangle()

factory = ShapeFactory()
shape1 = factory.create_shape('circle')
shape2 = factory.create_shape('square')
```
Here, `ShapeFactory` creates related shape objects (circles, squares, triangles) without needing to know their specific classes, as it relies on the `shape_type` parameter.

The statement <mark>when we need to create objects that belong to a family, but we don't care about the specific implementation</mark> simply means that we want to create objects that share a common behavior, without focusing on the details of how they're built. Let's see a small example:
```python
class Shape(ABC):
    @abstractmethod
    def draw(self):
        pass

class Circle(Shape):
    def draw(self):
        return "Drawing a circle"

class Square(Shape):
    def draw(self):
        return "Drawing a square"
```
Here, we're creating shapes that belong to the `Shape` family. We don't care about the specific implementation (e.g., how the circle or square is drawn) but we care about the common interface (the `draw` method). The `ShapeFactory` creates the objects, and we can use them without knowing their details:

```python
factory = ShapeFactory()
shape1 = factory.create_shape('circle')
shape2 = factory.create_shape('square')

shape1.draw()  # Output: Drawing a circle
shape2.draw()  # Output: Drawing a square
```
One can create and use shapes without knowing their specific classes or implementations, focusing on their shared behavior through the `Shape` interface.

Now, let's understand everything together with the following example:
```python
from abc import ABC
from abc import abstractmethod

class Engine(ABC):
    @abstractmethod
    def description(self):
        pass

class Car(ABC):
    @abstractmethod
    def assemble(self):
        pass

```

Concrete classes for `Hybrid`, `Electric`, and `Gasoline` engines:
```python
class HybridEngine(Engine):
    def description(self):
        return "hybrid engine"

class ElectricEngine(Engine):
    def description(self):
        return "electric engine"

class GasolineEngine(Engine):
    def description(self):
        return "gasoline engine"
```

Implementing concrete classes for `Car` with different engines:
```python
class HybridCar(Car):
    def __init__(self, engine: Engine):
        self.engine = engine

    def assemble(self):
        return f"Assembling a car with a {self.engine.description()}"

class ElectricCar(Car):
    def __init__(self, engine: Engine):
        self.engine = engine

    def assemble(self):
        return f"Assembling a car with a {self.engine.description()}"

class GasolineCar(Car):
    def __init__(self, engine: Engine):
        self.engine = engine

    def assemble(self):
        return f"Assembling a car with a {self.engine.description()}"

```

Abstract Factory for creating cars:
```python
class CarFactory(ABC):
    @abstractmethod
    def create_car(self) -> Car:
        pass
```

Concrete factory classes for `Hybrid`, `Electric`, and `Gasoline` cars:
```python
class HybridCarFactory(CarFactory):
    def create_car(self) -> Car:
        return HybridCar(HybridEngine())

class ElectricCarFactory(CarFactory):
    def create_car(self) -> Car:
        return ElectricCar(ElectricEngine())

class GasolineCarFactory(CarFactory):
    def create_car(self) -> Car:
        return GasolineCar(GasolineEngine())
```

putting everything together:
```python
def client_code(car_factory: CarFactory):
    car = car_factory.create_car()
    print(car.assemble())

hybrid_factory = HybridCarFactory()
electric_factory = ElectricCarFactory()
gasoline_factory = GasolineCarFactory()

client_code(hybrid_factory)    # Output: Assembling a car with a hybrid engine
client_code(electric_factory)  # Output: Assembling a car with a electric engine
client_code(gasoline_factory)  # Output: Assembling a car with a gasoline engine
```
The Abstract Factory pattern allows us to create cars with different engines without specifying their concrete classes, making it easy to add new types of engines or cars in the future.

Now, let's understand the difference between Abstract Factory and Factory Method.
1. Abstract Factory:
- It's about creating families of related objects.
- Abstract Factory contains multiple Factory Methods for creating different types of products.
- Clients use the factory object to create objects of different types that belong to a specific family.

2. Factory Method:
- It's about creating one type of object.
- Factory Method defines a single method for object creation.
- Subclasses decide which class to instantiate. Clients use the Factory Method to create objects without knowing the actual class being instantiated.

In summary, Abstract Factory is an extension of Factory Method that can create multiple related objects, while Factory Method focuses on creating a single type of object.

Hope the post have created some value. Peace!