---
title: "Command with examples in Python"
date: 2024-02-17T22:48:29+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/command.png
    alt: "command"
tags: ["design-patterns"]
---

The Command design pattern is a way to organize actions in software so that the requests (like user commands or system operations) are turned into objects. This makes it easier to manage and modify these requests, like putting them in a queue or undoing them. It also helps in separating the part of the software that asks for something to be done from the part that actually does it.

Imagine a restaurant where customers (the client) give their orders (the command) to a waiter (the invoker) who then forwards the orders to the kitchen (the receiver) to prepare the meal. In this scenario, the order is an object which contains all the information needed to prepare the meal. The kitchen doesn't need to know who the customer is; it just needs to know what to cook, which is what the order object encapsulates.

Here is a simplified example in Python

```python
class Car:
    def start(self):
        print("Car has started.")

    def stop(self):
        print("Car has stopped.")

class Command:
    def execute(self):
        pass

class StartCarCommand(Command):
    def __init__(self, car):
        self.car = car

    def execute(self):
        self.car.start()

class StopCarCommand(Command):
    def __init__(self, car):
        self.car = car

    def execute(self):
        self.car.stop()

# Client code
car = Car()
start_command = StartCarCommand(car)
stop_command = StopCarCommand(car)

# Invoker
class CarRemote:
    def submit(self, command):
        command.execute()

remote = CarRemote()
remote.submit(start_command)
remote.submit(stop_command)
```

Output:
```
Car has started.
Car has stopped.
```

In this code example, the Command pattern is used to control a car's operations (starting and stopping) through command objects (`StartCarCommand` and `StopCarCommand`). Each command encapsulates an action and its recipient (the `Car` object). This setup allows for flexible command execution via the `CarRemote` (the invoker), which can call different commands without knowing the details of how these actions are carried out. This separation of concerns makes it easier to add new commands, change the car's functionality, or extend the remote's capabilities without altering the existing code structure, demonstrating the Command pattern's usefulness in organizing and extending functionalities systematically.

A common real-world use case for the Command design pattern is in implementing undo and redo functionalities in applications like text editors, graphic design tools, or any kind of software that manipulates data or documents. In such applications, each action performed by the user, such as typing text, changing color, moving objects, or resizing elements, is encapsulated in a command object with a specific execute method for performing the action and an undo method for reversing it.

This approach allows the software to maintain a history of actions executed by the user. When the user requests an undo, the software can simply call the undo method on the most recent command object to revert the last action. Similarly, redo operations can re-execute the command. This system makes it easy to add new types of actions, as each action is encapsulated in its own command class, without altering the core functionality of the application. It ensures high flexibility and scalability in managing user interactions and data manipulations.