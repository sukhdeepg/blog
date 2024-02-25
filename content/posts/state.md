---
title: "State with examples in Python"
date: 2024-02-25T20:24:32+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/state.png
    alt: "state"
tags: ["design-patterns"]
---

This one can be bit tricky to understand first, but please read through the complete post, you'll get it.

The State design pattern is a method used in programming to allow an object to behave differently depending on its internal condition (refers to the current situation or status of an object, determined by its properties or attributes.) or "state". This pattern involves creating different "state" objects for each possible condition, and a main object, called the "context", which changes its behavior based on whichever state object is currently active. Instead of the context object needing to keep track of its state using conditions or flags, it simply delegates behavior to its current state object. This makes the code cleaner and easier to understand, as each state can be managed independently, and the main object doesn't need complex logic to handle its different behaviors.

Think of a vending machine that operates differently based on its current state: if the machine is in a "ready" state, it waits for customer input; if it's in a "selection made" state, it asks for money; and if it's in a "dispensing" state, it provides the product and returns to the "ready" state. The vending machine behaves differently depending on its internal state, but the way we interact with it remains consistent.

Let's understand further with Python example:

Here, the `Car` class that can be in different states like `Parked`, `Driving`, or `Stopped`. Depending on the state, the `drive` and `stop` methods of the `Car` class behave differently. Each state is represented by a separate class that implements the same interface, and the Car class changes its behavior by switching between these state instances.

```python
class State:
    def handle_drive(self):
        pass

    def handle_stop(self):
        pass

class ParkedState(State):
    def handle_drive(self):
        print("Switching to Driving state")
        return DrivingState()

    def handle_stop(self):
        print("Already parked")
        return self

class DrivingState(State):
    def handle_drive(self):
        print("Already driving")
        return self

    def handle_stop(self):
        print("Switching to Parked state")
        return ParkedState()

class Car:
    def __init__(self):
        self.state = ParkedState()

    def drive(self):
        self.state = self.state.handle_drive()

    def stop(self):
        self.state = self.state.handle_stop()

car = Car()
car.drive()
car.stop()
```

Output:
```text
Switching to Driving state
Switching to Parked state
```

In backend engineering, a common real-world example of the State design pattern is in the management of a user's session on a website. A user session can have various states such as "Logged Out", "Logged In", "Idle", or "Expired". The session object (context) behaves differently depending on its current state: when "Logged Out", it might only allow access to public pages; when "Logged In", it grants access to protected resources; when "Idle", it might send reminders or prompts to the user; and when "Expired", it requires the user to log in again.

Each of these states is represented by a separate state object that knows how to handle requests in that specific state. The session context delegates requests to its current state object, which handles the request based on the rules for that state. This modularizes the code and makes it clearer and easier to manage, as each state's behavior is encapsulated in its own class.
