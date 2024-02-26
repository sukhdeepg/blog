---
title: "Strategy with examples in Python"
date: 2024-02-26T17:19:34+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/strategy.png
    alt: "strategy"
tags: ["design-patterns"]
---

The Strategy design pattern lets us change the way an object behaves while the program is running. Imagine having a video game character that can switch tools like a hammer, a sword, or a shield based on what we choose during the game. Similarly, by using the Strategy pattern, we can change how an object acts on the fly, without stopping or changing the rest of our program.

Consider a navigation app that suggests routes to the destination. The app can change the strategy based on the preference of the user: fastest route, shortest route, or least traffic. These strategies can be switched easily without altering the user's interaction with the app.

Let's understand the above with a Python example:

```python
class BrakeBehavior:
    def apply_brake(self):
        pass

class NormalBrake(BrakeBehavior):
    def apply_brake(self):
        return "Normal braking applied"

class ABSBrake(BrakeBehavior):
    def apply_brake(self):
        return "ABS braking applied"

class Car:
    def __init__(self, brake_behavior: BrakeBehavior):
        self.brake_behavior = brake_behavior

    def apply_brake(self):
        return self.brake_behavior.apply_brake()

    # Method to change the brake behavior at runtime
    def set_brake_behavior(self, new_brake_behavior: BrakeBehavior):
        self.brake_behavior = new_brake_behavior

car = Car(NormalBrake())
print(car.apply_brake())

# Change the behavior at runtime
car.set_brake_behavior(ABSBrake())
print(car.apply_brake())
```

Output:
```text
Normal braking applied
ABS braking applied
```

the `Car` object starts with a normal braking behavior. Then, while the program is still running, we change the car's braking behavior to ABS braking by using the `set_brake_behavior` method. This demonstrates changing the object's behavior at runtime, which is the core concept of the Strategy design pattern.

The Strategy pattern is widely used in software engineering for features like compression, where different algorithms can be applied based on user choice or data type (e.g., ZIP, RAR). It's also common in payment processing systems, where different payment strategies can be applied depending on the payment method chosen by the user (e.g., credit card, PayPal, cryptocurrency).

Sorting algorithms in database systems or frameworks. Depending on the amount of data and its type, different sorting strategies can be applied (e.g., quick sort, merge sort, bubble sort) to optimize performance and resource usage without changing the code that uses the sorting functionality.