---
title: "Iterator with examples in Python"
date: 2024-02-20T08:27:41+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/iterator.png
    alt: "iterator"
tags: ["design-patterns"]
---

The Iterator design pattern provides a standard way to loop through a collection of objects without exposing the underlying representation (array, list, map, etc.). It allows us to access elements sequentially without needing to understand the inner workings of the collection.

Imagine we're at a pancake house with a menu of different pancake types. We want to look through all the pancake types one by one to decide which one to order. The menu acts as an iterator in this scenario. We don't need to know how the pancakes are stored in the kitchen or how the menu is organized; we just flip through the pages (or items), considering each option sequentially until we find what we like.

```python
class CarCollection:
    def __init__(self):
        self._cars = []

    def add_car(self, car):
        self._cars.append(car)

    def __iter__(self):
        return self.CarIterator(self._cars)

    class CarIterator:
        def __init__(self, cars):
            self._cars = cars
            self._index = 0

        def __next__(self):
            try:
                car = self._cars[self._index]
                self._index += 1
                return car
            except IndexError:
                raise StopIteration()

# Usage:
car_collection = CarCollection()
car_collection.add_car('Toyota')
car_collection.add_car('Honda')
car_collection.add_car('Ford')

for car in car_collection:
    print(car)
```

Output:
```text
Toyota
Honda
Ford
```

In this example, `CarCollection` is a collection of cars, and `CarIterator` is an iterator for this collection. This setup lets us loop through all the cars in `car_collection` without knowing how they are stored internally.

The Iterator pattern is widely used in software development, particularly in the design of collections in programming languages and frameworks. For example:

1. **Java Collections Framework (JCF):** The JCF uses the Iterator pattern extensively to allow users to traverse through sets, lists, and maps without knowing their internal representations.

2. **Python Collections**: The Collections Module offers specialized container data types like `Counter`, `Deque`, and `OrderedDict`, complementing basic types such as lists and dictionaries. Python's design inherently supports the Iterator pattern; built-in structures and those from the Collections Module are iterable, allowing seamless data traversal using the `for` loop or by creating iterators with `iter()`. For example, iterating over a list:

```python
my_list = [1, 2, 3]
for item in my_list:
    print(item)
```

Here, Python uses the iterator protocol behind the scenes, similar to how one might iterate over collections in other languages.

3. **Database Query Results:** When we execute a query that returns multiple records, the returned object (like a ResultSet in Java) often implements the Iterator pattern to let us go through each record one by one.

3. **File Systems:** When we need to list all files in a directory, the iterator pattern is used to go through each file without needing to know how the file list is implemented internally.

These examples demonstrate how the Iterator pattern facilitates the separation of concerns by hiding complex structures and providing a simple interface to traverse a collection of objects.
