---
title: "Template Method with examples in Python"
date: 2024-02-27T23:13:18+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/template_method.png
    alt: "template_method"
tags: ["design-patterns"]
---

The Template Method design pattern is a behavioral design pattern that defines the program skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure. In simpler terms, it’s like a recipe with certain steps defined and fixed and allows the child classes to implement the specifics of these steps.

Imagine the process of making a sandwich. The steps might include gathering ingredients, putting ingredients between bread, and serving the sandwich. These steps form the "template" for making a sandwich. However, the specific ingredients (like vegetarian or non vegetarian options) can vary. Each type of sandwich will follow the same basic steps, but the specifics can be customized.

Let's understand this with an example in Python:

```python
from abc import ABC, abstractmethod

class Car(ABC):
    # Template method
    def start_drive_stop(self):
        self.start()
        self.drive()
        self.stop()
    
    @abstractmethod
    def start(self):
        pass
    
    @abstractmethod
    def drive(self):
        pass

    @abstractmethod
    def stop(self):
        pass

class SportsCar(Car):
    def start(self):
        print("Sports car starting with roar")
    
    def drive(self):
        print("Sports car driving fast")
    
    def stop(self):
        print("Sports car stopping")

class FamilyCar(Car):
    def start(self):
        print("Family car starting quietly")
    
    def drive(self):
        print("Family car driving safely")
    
    def stop(self):
        print("Family car stopping smoothly")

sports_car = SportsCar()
sports_car.start_drive_stop()

family_car = FamilyCar()
family_car.start_drive_stop()
```

Output:
```text
Sports car starting with roar
Sports car driving fast
Sports car stopping
Family car starting quietly
Family car driving safely
Family car stopping smoothly
```

The Template Method pattern is often used in frameworks. For example, in web application frameworks, there are common steps to handle HTTP requests, such as authentication, loading data, rendering views, and sending responses. The framework defines the order of these steps, but allows developers to customize the behavior of each step.

Also frequently used in data processing applications, where the skeleton of the processing algorithm is defined (e.g., reading data, processing data, and writing results), but the actual processing logic varies depending on the type of data or the specific requirements of the processing task.