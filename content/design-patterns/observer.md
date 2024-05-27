---
title: "Observer with examples in Python"
date: 2024-02-25T20:07:55+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/observer.png
    alt: "observer"
tags: ["design-patterns"]
---

The Observer design pattern is a behavioral design pattern where an object, known as the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods. It's commonly used to implement distributed event handling systems.

A real-world analogy for the Observer pattern is a subscription to a newspaper or magazine. In this analogy, the newspaper is the subject, and the subscribers are the observers. Whenever there is a new edition of the newspaper, all subscribers automatically receive it. If a subscriber decides to cancel their subscription, they stop receiving new editions.

Let's see an example in Python:

A car tracking system where the car's speed and fuel level are monitored. We'll have a `Car` class as the subject, and two observer classes: `SpeedAlert` and `FuelAlert`. The `SpeedAlert` observer will be notified when the car exceeds a certain speed limit, while `FuelAlert` will be notified when the fuel level drops below a certain threshold.

```python
class Car:  # Subject
    def __init__(self):
        self._speed = 0
        self._fuel_level = 100
        self._observers = []

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self):
        for observer in self._observers:
            observer.update(self)

    def set_speed(self, speed):
        self._speed = speed
        self.notify()

    def set_fuel_level(self, level):
        self._fuel_level = level
        self.notify()

    @property
    def speed(self):
        return self._speed

    @property
    def fuel_level(self):
        return self._fuel_level

class SpeedAlert:  # Observer for speed
    def update(self, car):
        if car.speed > 100:  # Assuming 100 is the speed limit
            print(f"Speed Alert: Your speed is {car.speed} km/h, which exceeds the safe speed limit!")

class FuelAlert:  # Observer for fuel
    def update(self, car):
        if car.fuel_level < 20:  # Assuming 20 is the low fuel threshold
            print(f"Fuel Alert: You are running low on fuel. Only {car.fuel_level}% remaining!")

car = Car()
speed_alert = SpeedAlert()
fuel_alert = FuelAlert()

car.attach(speed_alert)
car.attach(fuel_alert)

car.set_speed(120)  # triggers SpeedAlert
car.set_fuel_level(15)  # triggers FuelAlert
```

Output:
```text
Speed Alert: Your speed is 120 km/h, which exceeds the safe speed limit!
Speed Alert: Your speed is 120 km/h, which exceeds the safe speed limit!
Fuel Alert: You are running low on fuel. Only 15% remaining!
```

In software engineering, the Observer pattern is most frequently used in event management systems, such as GUI toolkits. For example, in a web application, this pattern is used to listen to user events like clicks or mouse movements and update the view accordingly without the user having to manually refresh the page.

Another common real-world application of the Observer pattern is in the implementation of Model-View-Controller (MVC) architecture, particularly for web applications. In MVC, the Model acts as the subject, while Views act as observers. When the Model changes (for instance, a database update), it notifies the Views, leading to an automatic update of the user interface.