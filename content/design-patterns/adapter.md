---
title: "Adapter with examples in Python"
date: 2023-05-24T09:33:49+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/adapter.png
    alt: "adapter"
tags: ["design-patterns"]
---

The adapter design pattern is a structural design pattern that allows objects that don't initially know how to interact with each other (due to differences in their communication methods) to still cooperate. This pattern introduces a wrapper class (an "adapter") which translates the interface of one class into an interface expected by clients.

In real world, when one of our electrical appliance has a plug that won't fit in the socket due to the appliance having different norm than the other appliances, we make use of an adapter to overcome this and use the appliance. Here, this adapter is the adapter pattern.

Let's understand this with an example:
```python
class Car:
    def __init__(self, model):
        self.model = model

    def start_engine(self):
        return f"{self.model}'s engine started."

    def refuel(self):
        return f"Refuelling {self.model}."
```

Here, we have an `ElectricCar` with different interface than the `Car`:
```python
class ElectricCar:
    def __init__(self, model):
        self.model = model

    def start_electric_engine(self):
        return f"{self.model}'s electric engine started."

    def recharge_battery(self):
        return f"Recharging {self.model}."
```

Our existing system doesn't know how to interact with `ElectricCar` object as it only knows how to work with `Car` object. To solve this, we'll use the Adapter design pattern.

Let's create an `ElectricCarAdapter` because here we can see that `Car` and `ElectricCar` have similar purpose.
```python
class ElectricCarAdapter:
    def __init__(self, electric_car):
        self.electric_car = electric_car

    def start_engine(self):
        return self.electric_car.start_electric_engine()

    def refuel(self):
        return self.electric_car.recharge_battery()
```

Now, we can use `ElectricCar` object in the existing system similar to `Car` object.

```python
def client_code(car):
    print(car.start_engine())
    print(car.refuel())

if __name__ == "__main__":
    my_car = Car("PetrolCar")
    client_code(my_car)

    my_electric_car = ElectricCarAdapter(ElectricCar("ModernEV"))
    client_code(my_electric_car)
```

Output:
```text
PetrolCar's engine started.
Refuelling PetrolCar.
ModernEV's electric engine started.
Recharging ModernEV.
```

Here, we saw that how Adapter pattern can enable code to work with classes that otherwise wouldn't be compatible due to their interfaces.

Some real world scenarios where Adapter pattern could be used:
1. Legacy and modern systems: When there is a need to integrate our modern system with a very old legacy system where rewritting the complete legacy system is not feasible, we can use the Adapter pattern to create an interface to enable interaction between legacy and modern systems.

2. Working with Third-Party libraries: Sometimes, a library has an interface that doesn’t match our system’s interface. An adapter class can help translate the interface of the third-party library to the interface our system expects.

Hope the post have created some value. Peace!