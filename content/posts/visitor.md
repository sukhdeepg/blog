---
title: "Visitor with examples in Python"
date: 2024-03-01T21:49:21+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/visitor.png
    alt: "visitor"
tags: ["design-patterns"]
---

The Visitor design pattern is like a tool that lets us add new features to our code without changing the original code. Imagine we have a bunch of different types of files on our computer (like documents, music, and videos), and we want to perform various tasks on them, like opening or scanning for viruses. Instead of adding new code to each file type, we create a "visitor" – a separate set of instructions or tool – that can interact with each type of file to perform the task. This way, our original files remain unchanged, and we can easily add new actions without messing with the existing setup.

In backend engineering, think of it as if we have different types of data (like user data, product data, etc.) stored in our system. We might need to perform tasks like validating or formatting this data differently. Instead of changing the original data structures, we create a "visitor" (a piece of code) that goes through each data type and performs the needed task. This makes our system more flexible and easier to update or maintain, as we can add new operations without altering the core structures of our data.

Imagine a tax inspector visiting different types of stores in a mall to assess taxes. Each store (like a bookstore, a restaurant, or a jewelry shop) handles the tax inspection differently due to their different types of business. However, the tax inspector (the "visitor") can visit each store and apply the necessary tax rules without the stores needing to know the details of tax assessment processes. Each store just needs to allow the inspector to visit.

Let's understand this further with an example in Python:

```python
class CarElement:
    def accept(self, visitor):
        pass

class Body(CarElement):
    def accept(self, visitor):
        visitor.visitBody(self)

class Engine(CarElement):
    def accept(self, visitor):
        visitor.visitEngine(self)

class Car(CarElement):
    def __init__(self):
        self.elements = [Engine(), Body()]
    
    def accept(self, visitor):
        for element in self.elements:
            element.accept(visitor)
        visitor.visitCar(self)

class CarElementVisitor:
    def visitBody(self, body):
        print("Checking car body.")
    
    def visitEngine(self, engine):
        print("Checking engine.")

    def visitCar(self, car):
        print("Inspecting overall car.")

visitor = CarElementVisitor()
car = Car()
car.accept(visitor)
```

Output:
```text
Checking engine.
Checking car body.
Inspecting overall car.
```

Here we have different parts of a car (such as the Body and Engine) represented as classes, each inheriting from a common interface, `CarElement`. This setup allows various car parts to be treated uniformly. Each part class has an `accept` method that accepts a visitor object and calls a visit method on it, passing itself as an argument. This is how the car parts "accept" the visitor, allowing the visitor to perform specific actions on them.

The `CarElementVisitor` class is the visitor, equipped with different methods (`visitBody`, `visitEngine`, `visitCar`) to handle different types of car elements. These methods define what to do when visiting each type of part, like checking the car's body or engine. A `Car` class represents the entire car and contains a collection of car parts. It also has an `accept` method, which lets the visitor visit each part of the car. In the end, when we create a `Car` object and a `CarElementVisitor` object, and let the car accept the visitor, it results in the visitor traversing and performing operations on each part of the car, demonstrating how we can perform various actions on the car's components without changing the car's design or structure. This makes it easy to add new features without altering existing code.

The Visitor pattern is often used in compilers for programming languages. In this context, the compiler uses the visitor to traverse an abstract syntax tree (AST) representing the source code. Each node in the tree may represent a different structure (e.g., expressions, statements, function calls). The visitor pattern allows the compiler to perform operations such as type checking, code optimization (constant folding or dead code elimination), or code generation on these nodes without changing the classes of the elements of the tree.