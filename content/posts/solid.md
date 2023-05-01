---
title: "SOLID Principles with examples in Python"
date: 2023-03-21T23:07:07+05:30
draft: false
showToc: true
TocOpen: true
cover:
    image: img/solid_principles.png
    alt: "solid_principles"
tags: ["fundamentals", "low-level-design"]
---

When we start our programming journey, with continuous practice and learning, writing code becomes easier. But, as we advance in our careers, it becomes equally important to learn how to maintain and help others maintain what we are writing.
<br/>

### 1. Single Responsibility Principle
Easy to understand. Every module, class, or function should only have a single responsibility or only one reason to change. But it’s difficult to practically implement because lines can get blurry during implementation.

To simplify this, Uncle Bob says that *"This principle is about people"* in this [blog](https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html).

Let’s understand with an example
```python
class Payment:
    
    # process the payment
    def process(self):
        pass
    
    # save the payment
    def save(self):
        pass
    
    # retrieve the payment information
    def retrieve(self):
        pass
    
    # return analytics data related to payment. E.g. processing time of payment
    def analytics(self):
        pass
    
    # check if the information for payment is correct or not. E.g. card number, CVV, etc
    def check(self):
        pass
```

As we can see, this class is performing a lot of functions for a given payment and has more than one reason to change. What if we have different people using these functionalities? If one person thinks to change the `check` function logic and return `field` to `bool` mapping `dict` e.g `{“is_cvv_valid”: True}` instead of `list` of `field` and `bool` `tuple` e.g. `[("is_cvv_valid", True)]`, this will affect the processing logic and eventually, analytics will create panic!

It will be better if each functionality is isolated and handled by a single team or individual in order to avoid any dependency and compatibility issues. Each functionality will have a standard output format. So, even if the internal logic changes for a functionality, it won’t affect the other dependent functionalities and will also have a single responsibility and reason to change. This will make the code more cohesive and easier to maintain.

```python
class ProcessPayment:
    
    def process(self):
        pass
    
class SavePayment:
    
    def save(self):
        pass

class RetrievePayment:
    
    def retrieve(self):
        pass
    
class AnalyticsPayment:
    
    def analytics(self):
        pass
    
class SecCheckPayment:
    
    def security_check(self):
        pass
```
<br/>

### 2. Open-closed Principle
Open for extension but closed for modification. *Extension* means that we’re extending the functionality of our code. *Modification* means that we’re modifying our existing code.

Now, which sounds more risky? modification, right? Because when we write our code, test it, and deploy it, we should not go back and modify it, as this can lead to instability, create bugs, etc.

In Python (and in many other languages), we can make use of an abstract base class to help us extend the functionality of our code.

Let’s understand with an example

```python
from abc import ABC, abstractmethod

class Hardware(ABC):
    
    @abstractmethod
    def functionality():
        pass

class Monitor(Hardware):
    
    def functionality(self):
        print('To display information on the screen.')

class Mouse(Hardware):
    
    def functionality(self):
        print('To move cursor on the screen and click on elements.')

class Keyboard(Hardware):
    
    def functionality(self):
        print('To help type the required information.')

mon = Monitor()
mou = Mouse()
key = Keyboard()

mon.functionality()
mou.functionality()
key.functionality()
```

Here, if we need to add functionality for Printer, we don’t need to modify any existing class or function, we can simply extend the Hardware class and create the functionality.

```python
class Printer(Hardware):
    
    def functionality(self):
        print('To print information on the paper.')
```
<br/>

### 3. Liskov Substitution Principle
If we have an object of superclass (A) and an object of child class (B), then we should be able to replace A with B without affecting the existing behaviour of the program.

Continuing the example from the Open-closed principle, if we want to create a function that takes the `Hardware` and prints its functionality, we don’t want to create `if` `elif` `else` condition blocks to decide what to print. Instead, it will be much cleaner to create a generic function that just takes an object and prints the functionality.

```python
from abc import ABC, abstractmethod

class Hardware(ABC):
    
    @abstractmethod
    def functionality():
        pass

class Monitor(Hardware):
    
    def functionality(self):
        print('To display information on the screen.')

class Mouse(Hardware):
    
    def functionality(self):
        print('To move cursor on the screen and click on elements.')

class Keyboard(Hardware):
    
    def functionality(self):
        print('To help type the required information.')
        
class Printer(Hardware):
    
    def functionality(self):
        print('To print information on the paper.')

def print_functionality(h: Hardware):
    h.functionality()

mon = Monitor()
mou = Mouse()
key = Keyboard()
pri = Printer()

print_functionality(mon)
print_functionality(mou)
print_functionality(key)
print_functionality(pri)
```

In the `print_functionality` function, we can easily replace the object of the `Hardware` class with objects of the `Monitor`, `Mouse`, `Keyboard`, `Printer` classes.
<br/>

### 4. Interface Segregation Principle
> The interface segregation principle (ISP) states that no code should be forced to depend on methods it does not use. [Source](https://en.wikipedia.org/wiki/Interface_segregation_principle#cite_note-ASD-1).

If we add the `firmware_update` function to our `Hardware` class, it would mean that, all our child classes would need to have the `firmware_update` function.

```python
class Hardware(ABC):
    
    @abstractmethod
    def functionality():
        pass
    
    @abstractmethod
    def firmware_update():
        pass
```

Now, this `firmware_update` function will not be used by the `mouse` and `keyboard` usually. So, why do these classes even need to have this function? This violates the ISP.
To avoid this, we can have the following update

```python
from abc import ABC, abstractmethod

class Hardware(ABC):
    
    @abstractmethod
    def functionality():
        pass
    
class Firmware(ABC):
    
    @abstractmethod
    def update():
        pass

class Monitor(Hardware, Firmware):
    
    def functionality(self):
        print('To display information on the screen.')
        
    def update():
        print('Updating firmware.')

class Mouse(Hardware):
    
    def functionality(self):
        print('To move cursor on the screen and click on elements.')

class Keyboard(Hardware):
    
    def functionality(self):
        print('To help type the required information.')
        
class Printer(Hardware, Firmware):
    
    def functionality(self):
        print('To print information on the paper.')
        
    def update(self):
        print('Updating firmware.')
```
<br/>

### 5. Dependency Inversion Principle
High-level modules or classes should not depend on low-level modules (concrete implementations) or classes. High-modules should depend on abstractions or interfaces.

Let’s see example for high-level and low-level class

```python
from abc import ABC, abstractmethod

class MusicPlayer:
    
    def play(self):
        music_service_a = MusicServiceA()
        music_service_a.play()
        
class MusicServiceA:
    
    def play(self):
        print('Playing music from MusicServiceA.')
        
mp = MusicPlayer()
mp.play()
```

`MusicPlayer` is the high-level class and `MusicServiceA` is the low-level class. Here, `MusicPlayer` is directly dependent on the `MusicServiceA` class. If tomorrow, we need another service to play music from, we would need to modify the `MusicPlayer` class which violates the OCP. To avoid this dependency, we can create a `MusicService` abstract class and pass it to the `MusicPlayer`.

```python
from abc import ABC, abstractmethod

class MusicPlayer:
    
    def __init__(self, music_service):
        self.music_service = music_service
    
    def play(self):
        self.music_service.play()
        
class MusicService(ABC):
    
    @abstractmethod
    def play(self):
        pass
        
class MusicServiceA(MusicService):
    
    def play(self):
        print('Playing music from MusicServiceA.')
        
class MusicServiceB(MusicService):
    
    def play(self):
        print('Playing music from MusicServiceB.')

msa = MusicServiceA()
msb = MusicServiceB()
mp1 = MusicPlayer(msa)
mp2 = MusicPlayer(msb)
mp1.play()
mp2.play()
```  
<br/>

### Conclusion
We covered all the SOLID principles with Python examples (dos and don'ts) and simplified the definitions associated with the principles.

Hope the post have created some value. Peace!