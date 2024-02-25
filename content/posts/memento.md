---
title: "Memento with examples in Python"
date: 2024-02-25T16:02:41+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/memento.png
    alt: "memento"
tags: ["design-patterns"]
---

The Memento design pattern is like a save point for an object's information, allowing that object to be returned to its previous state later on. This is similar to saving a game and then loading it back up; we get everything back as it was, without needing to know how the game internally manages all its details. This approach is very useful in making features like the 'undo' option in many software applications, as it helps reverse actions without disrupting the private workings of the objects involved.

Imagine we are writing a document using a text editor, and we can press "Ctrl + Z" to undo our last action. In this scenario, each state of the document before a change is made acts as a "memento." The text editor saves these states without exposing the details of the content (encapsulation). The encapsulation here means that the text editor keeps a record of its changes in a way that the inner workings are not shown or affected – this is similar to keeping personal notes private while still being able to refer back to them when needed. When we press undo, the editor restores the document to the last saved state.

Let's see an example in Python for this:

```python
class CarMemento:
    def __init__(self, state):
        self._state = state

    def get_state(self):
        return self._state

class Car:
    def __init__(self):
        self._state = ""

    def set_state(self, state):
        self._state = state

    def save_state_to_memento(self):
        return CarMemento(self._state)

    def get_state_from_memento(self, memento):
        self._state = memento.get_state()

car = Car()
car.set_state("Engine on")
saved_states = []
saved_states.append(car.save_state_to_memento())
car.set_state("Engine off")
car.get_state_from_memento(saved_states[0])  # Restores to "Engine on"
print(f"current state: {car._state}")
```

Output:
```text
current state: Engine on
```

In software engineering, the Memento pattern is commonly used in the implementation of undo mechanisms in applications like text editors, graphic editors, and browsers. It allows these applications to store snapshots of their current state at various points in time and restore them as needed without revealing the internals of their state.

Another frequent use case for the Memento pattern is in game development, where it can be used to save the state of a game, allowing players to save their progress and later reload it from exactly the same point. This includes saving the state of characters, levels, and items without exposing the complex internals of how these are maintained.