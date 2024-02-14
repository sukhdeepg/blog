---
title: "Chain of Responsibility with examples in Python"
date: 2024-02-14T10:18:29+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/chain_of_responsibility.png
    alt: "decorator"
tags: ["design-patterns"]
---

The Chain of Responsibility pattern is a design approach in programming that lets us pass requests through a series of processing units or "handlers". Each handler is a piece of code or a function that has the chance to process the request, or pass it along to the next handler in the sequence. This method helps in organizing code in a way that separates the request sender from its processors, allowing for dynamic handling of requests based on runtime conditions. This pattern promotes the principle of loose coupling and is particularly useful when the exact handler is not known in advance.

Imagine a customer support system in a company. When a customer raises a complaint or query, it first reaches the front desk (the first level of support). If the front desk can't solve the issue, the query is passed to the technical support team (the second level). If the technical team also can't solve it, the query is finally escalated to the engineering team (the third level). Each level in this chain has the opportunity to resolve the issue or pass it along to the next level.

Let's illustrate the Chain of Responsibility pattern with a simple Python example that simulates a car service chain. In this example, each service station checks a particular aspect of the car (e.g., Oil Check, Air Filter Check, and Brake Check) and either handles the task or passes it to the next service station in the chain.

```python
class Handler:
    """Abstract handler"""
    def __init__(self, successor=None):
        self._successor = successor

    def handle_request(self, request):
        raise NotImplementedError('Must provide implementation in subclass!')

class OilCheckHandler(Handler):
    def handle_request(self, request):
        if request == "Oil Check":
            print("Oil Check Done!")
        elif self._successor is not None:
            self._successor.handle_request(request)

class AirFilterCheckHandler(Handler):
    def handle_request(self, request):
        if request == "Air Filter Check":
            print("Air Filter Check Done!")
        elif self._successor is not None:
            self._successor.handle_request(request)

class BrakeCheckHandler(Handler):
    def handle_request(self, request):
        if request == "Brake Check":
            print("Brake Check Done!")
        elif self._successor is not None:
            self._successor.handle_request(request)

# Creating the chain
chain = OilCheckHandler(AirFilterCheckHandler(BrakeCheckHandler()))

# Sending requests
chain.handle_request("Oil Check")
chain.handle_request("Air Filter Check")
chain.handle_request("Brake Check")
```

Output:
```text
Oil Check Done!
Air Filter Check Done!
Brake Check Done!
```

This code simulates a scenario where a car goes through various service checks. Each handler in the chain has a specific task to perform and knows how to pass tasks it cannot handle to the next handler.

A frequent real-world use case for the Chain of Responsibility pattern is in the processing of financial transactions, particularly in payment authorization systems. In such systems, a transaction request might need to pass through several checks or validations before it can be approved. These checks might include verifying the account balance, checking for fraud patterns, ensuring compliance with legal regulations, and finally, processing the payment itself.

Each of these checks represents a handler in the chain. The transaction request is passed along this chain until it either gets approved (processed by a handler) or rejected (fails a check at some handler). This design allows for flexible addition or removal of checks without altering the core processing logic or affecting other checks, making the system highly adaptable to changing requirements or regulations.