---
title: "Proxy with examples in Python"
date: 2024-02-10T21:57:40+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/proxy.png
    alt: "decorator"
tags: ["design-patterns"]
---

The Proxy Design Pattern is like having a gatekeeper for an object, where the gatekeeper controls who can access the object and how they can use it. It's like having a security guard for a building; the guard checks who the person is and decides if they can enter, and might also keep track of who comes in and out. This pattern lets us add a layer around an object that handles these checks and controls without changing the object itself. So, it's a way to manage access and interactions with the object in a controlled manner.

Imagine we are trying to buy a ticket for a concert. Instead of buying the ticket directly from the concert hall, we go through a ticketing agent. This agent provides us with additional services such as finding the best seats, handling the payment process, and even giving us some advice on the event. Here, the ticketing agent acts as a proxy between us and the concert hall. The agent controls access to the concert hall's tickets and adds some level of indirection, which can be beneficial for both us and the concert hall.

In this example, we have a `Car` class, and we want to control access to this class with a `CarProxy` class.

```python
class Car:
    def drive(self):
        print("Car has been driven")

class CarProxy:
    def __init__(self, driver_age):
        self.driver_age = driver_age
        self.real_car = Car()
    
    def drive(self):
        if self.driver_age >= 18:
            self.real_car.drive()
        else:
            print("Sorry, the driver is too young to drive.")

# Usage
young_driver = CarProxy(driver_age=16)
young_driver.drive()

adult_driver = CarProxy(driver_age=25)
adult_driver.drive()
```

In this example, the `CarProxy` controls access to the `Car`'s drive method based on the driver's age, acting as a protective proxy.

Output:
```
Sorry, the driver is too young to drive.
Car has been driven
```

In software engineering, the Proxy Design Pattern is often applied to manage database connections efficiently, serving as a real-world example of its utility. A Database Connection Proxy acts as an intermediary between an application and its database, handling tasks like connection pooling to reduce the overhead of repeatedly opening and closing connections, caching frequent queries to improve performance, enforcing access control to enhance security, and logging queries for monitoring and analytics purposes. This approach is particularly beneficial in high-traffic scenarios, such as an e-commerce platform, where it ensures scalability, security, and performance by managing how the application interacts with the database, demonstrating the pattern's capability to offer a flexible and effective solution for resource management. ProxySQL is a good example of this.