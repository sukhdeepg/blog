---
title: "Flyweight with examples in Python"
date: 2024-02-07T20:51:28+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/flyweight.png
    alt: "decorator"
tags: ["design-patterns"]
---

The flyweight design pattern is a way to save memory by sharing as much data as possible with similar objects. It's like having a library where instead of buying a book every time we want to read it, we just borrow it, read it, and return it. This way, many people can read the book, but there's only one copy that everyone shares.

In real world, imagine we have a company that creates business cards. Instead of printing a new card for each employee, we have a template that has the company's logo, the font, and the design. When a new employee needs a card, we only change the name and contact details but use the same template for everything else. That template is like the shared part in the flyweight pattern.

Let's understand this with an example, say we have a program that manages a fleet of cars. Without the flyweight pattern, we might create a complete object for each car, which can take up a lot of memory if we have thousands of cars. But many cars share properties like model, brand, or color. With the flyweight pattern, we can create a class that only stores the shared data once and then create smaller, individual objects for each car that reference the shared data.

```python
class CarModel:
    # The Flyweight Class
    def __init__(self, brand, model, color):
        self.brand = brand
        self.model = model
        self.color = color

class Car:
    # The Context Class
    def __init__(self, vin, owner, car_model):
        self.vin = vin
        self.owner = owner
        self.car_model = car_model

# Flyweight Factory
class CarFactory:
    _models = {}

    def get_car_model(self, brand, model, color):
        # Returns an existing instance or creates a new one if it doesn't exist
        if (brand, model, color) not in self._models:
            self._models[(brand, model, color)] = CarModel(brand, model, color)
        return self._models[(brand, model, color)]

car_factory = CarFactory()

# Let's say we need to create two cars with the same model and color
car1 = Car("VIN12345", "Alice", car_factory.get_car_model("Tesla", "Model S", "White"))
car2 = Car("VIN67890", "Bob", car_factory.get_car_model("Tesla", "Model S", "White"))

# Both car1 and car2 share the same CarModel instance.
```

Practically in code, this pattern can be used in a video game (for this I've taken reference from [refectoring.guru](https://refactoring.guru/design-patterns/flyweight/python/example)'s tree example and pseudocode), we might have thousands of trees in the background. Instead of creating a separate object in memory for each tree, which could be very memory-intensive, we use the flyweight pattern. We create a single tree object and then reference it every time we need a new tree in the game's world. We only store the position of each tree uniquely. This saves memory and allows the game to run smoother on devices with less RAM.

This looks very similar to cache right? both aim to improve efficiency by reusing objects that are expensive to create. Here are few points around this:

1. **Reuse of Instances**: Just as a cache stores data so that future requests for that data can be served faster, the flyweight pattern keeps instances of similar objects that can be reused. This avoids the overhead of creating a new instance each time.

2. **Memory Savings**: Both patterns help save memory. A cache does this by storing data that can be reused, thereby avoiding the need to recompute or reload data from a slower part of the system. Similarly, the flyweight pattern stores common data externally and shares it among objects, thus reducing the memory footprint.

3. **Performance Improvement**: The use of caches can greatly speed up access to data that would otherwise take a long time to retrieve or compute. Similarly, the flyweight pattern can speed up programs by avoiding the need to instantiate many similar objects, which can be computationally expensive.

The difference is mainly in their intent and use cases:

- A **cache** is a general-purpose storage mechanism that can hold any kind of data and is typically used to store results of operations, computations, or network calls.
- The **flyweight pattern** is a design pattern specifically used in object-oriented programming when creating a large number of similar objects.

In essence, we could say that the flyweight pattern implements a form of caching for object instances. It's a more specialized form of caching that is focused on sharing object state to minimize memory usage, rather than speeding up data retrieval.

Now, let's understand 2 important states of flyweight pattern. Intrinsic and Extrinsic.
The **intrinsic state** refers to the information that is shared and does not vary between objects. This shared data is kept in the flyweight object and is independent of the flyweight's context, meaning that it is common to all objects and doesn't change from one object to another. The intrinsic state is what enables the memory efficiency of the flyweight pattern, as it is only stored once and referenced by all the individual objects that need it.

On the other hand, the **extrinsic state** consists of the information that varies between objects and is passed to the flyweight upon request. This state is context-specific and changes from one object to another. Since the extrinsic state is not shared, it must be stored externally and must be computed or applied each time it is used. In the flyweight pattern, this is the state that we would pass through method parameters when calling flyweight methods.

Example explaining both these states:
Here we have a class representing different types of trees in a forest. The type of tree (like 'Oak', 'Maple', etc.) represents the intrinsic state, which is shared among all trees of the same type. The position of each tree in the forest represents the extrinsic state, which is unique for each tree instance.
```python
# Flyweight class to store intrinsic state
class TreeType:
    def __init__(self, name, color, texture):
        self.name = name        # Intrinsic State
        self.color = color      # Intrinsic State
        self.texture = texture  # Intrinsic State

    def display(self, x, y):
        print(f"Displaying a {self.color} {self.name} tree at ({x}, {y}).")

# Factory to manage TreeType flyweight instances
class TreeFactory:
    _tree_types = {}

    @classmethod
    def get_tree_type(cls, name, color, texture):
        if (name, color, texture) not in cls._tree_types:
            cls._tree_types[(name, color, texture)] = TreeType(name, color, texture)
        return cls._tree_types[(name, color, texture)]

# Context class to store extrinsic state
class Tree:
    def __init__(self, x, y, tree_type):
        self.x = x              # Extrinsic State
        self.y = y              # Extrinsic State
        self.tree_type = tree_type

    def display(self):
        self.tree_type.display(self.x, self.y)

# Usage
# A forest class containing multiple tree instances
class Forest:
    def __init__(self):
        self.trees = []

    def plant_tree(self, x, y, name, color, texture):
        tree_type = TreeFactory.get_tree_type(name, color, texture)
        tree = Tree(x, y, tree_type)
        self.trees.append(tree)

    def display_forest(self):
        for tree in self.trees:
            tree.display()

# Client code
forest = Forest()
forest.plant_tree(1, 2, "Maple", "Red", "Rough")
forest.plant_tree(5, 3, "Oak", "Green", "Rough")
forest.plant_tree(10, 1, "Maple", "Red", "Rough")  # Reuses Maple tree type

forest.display_forest()
```
In this example:

- The `TreeType` class represents the flyweight which includes the intrinsic state (`name`, `color`, and `texture`).
- The `Tree` class represents the context which has the extrinsic state (`x` and `y` coordinates).
- `TreeFactory` is used to ensure that for each type of tree, only one `TreeType` instance is created and shared (flyweight).
- The `display` method of `TreeType` needs the extrinsic state to display the tree, which is provided by the `Tree`'s `display` method when it is called.

When we run this code, the `Forest` class will plant trees of different types at different locations, but it will reuse the `TreeType` instances wherever possible, demonstrating the flyweight pattern.
