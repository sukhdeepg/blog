---
title: "Mediator with examples in Python"
date: 2024-02-23T21:58:50+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/mediator.png
    alt: "mediator"
tags: ["design-patterns"]
---

The mediator design pattern is a behavioral design pattern that allows us to reduce chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object. This helps to decrease the coupling between classes of objects and the complexity of their relationships.

Imagine a typical airport control tower. The pilots do not communicate directly with each other; instead, they speak to the control tower. The control tower (the mediator) then directs the planes (the objects) when to take off or land, ensuring that no two planes attempt to use the runway at the same time. In this analogy, the control tower is the mediator facilitating communication between planes.

Let's see an example in Python

```python
class Mediator:
    def notify(self, sender, event):
        pass

class Car(Mediator):
    def __init__(self):
        self.components = []

    def add_component(self, component):
        self.components.append(component)

    def notify(self, sender, event):
        for component in self.components:
            if component is not sender:
                component.receive(event)

class Engine:
    def __init__(self, mediator):
        self.mediator = mediator

    def start(self):
        print("Engine started")
        self.mediator.notify(self, "ENGINE_STARTED")

    def receive(self, event):
        if event == "FUEL_LOW":
            print("Engine: Received notice of low fuel")

class FuelGauge:
    def __init__(self, mediator):
        self.mediator = mediator

    def low_fuel(self):
        print("Fuel Gauge: Fuel is low")
        self.mediator.notify(self, "FUEL_LOW")

    def receive(self, event):
        # FuelGauge might not need to react to other components' events
        pass

mediator = Car()
engine = Engine(mediator)
fuel_gauge = FuelGauge(mediator)
mediator.add_component(engine)
mediator.add_component(fuel_gauge)

fuel_gauge.low_fuel()  # This will notify the engine about the low fuel
engine.start()  # This could notify other components that the engine has started
```

Output:
```text
Fuel Gauge: Fuel is low
Engine: Received notice of low fuel
Engine started
```

In this example, `Car` acts as a mediator for the `Engine` and `FuelGauge` components. The components communicate with each other through the `Car` (mediator) instead of directly.

Common use case for the Mediator design pattern is in the implementation of event handling systems, particularly in web development frameworks like React or Angular. In these environments, the Mediator pattern can be employed to manage complex sets of interactions between various UI components. Instead of allowing each component to directly communicate with others, an event manager (the mediator) is used to handle events and coordinate the responses between components. This approach simplifies the communication logic, making the application easier to develop and maintain by centralizing the event handling logic, reducing direct dependencies among components, and improving the overall system modularity and reusability.