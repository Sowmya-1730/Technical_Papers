# SOLID Principles in Python with code samples

SOLID Principles are five important design principles in Object-Oritented programming that help developers build clean, maintainable, reusable and scalable software systems. These principles reduce code complexity and improve software quality by promoting better class design and separation of responsibilites.

- Single Responsibility Principle (S) 
- Open/ Closed Principles (O)
- Liskov Substitution Principle (L)
- Interface Segregation Principle (I)
- Dependency Inversion Principle (D)

## Single Responsibility Principle (S):
A class should only have one responsibility to taken care of.

### Sample Code
```python
# Bad Example
class Report:
    def generate_report(self):
        print("Generating report")
    def save_fig(self):
        print("Saving figure to file")


# Good Example
class Report:
    def generate_Report(self):
        print("Generating report")

class SaveFigure:
    def save_fig(self):
        print("Saving figure to file")
```


## Open/ Closed Principle (O):
Software entities should be open for extension but should be closed for modification.

### Sample Code
```python
# Bad Example
class Discount:
    def calculate(self, customer_type, amount):
        if customer_type == "regular":
            return amount * 0.1
        if customer_type == "premium":
            return amount * 0.2

# Good Example
class Discount:
    def calculate(self, amount):
        pass

class Regular:
    def calculate(self, amount):
        return amount * 0.1
    
class Premium:
    def calculate(self, amount):
        return amount * 0.2
```


## Liskov Substitution Principle (L):
Objects of a subclass should be replaceable with objects of parent class without affecting program correctness.
### Sample Code
```python
# Bad Example
class Bird:
    def fly(self):
        print("Flying")

class Ostrich(Bird):
    raise Exception("Ostrich cannot fly")

# Good Example
class Bird:
    pass

class FlyingBird(Bird):
    def flying(self):
        print("Flying")

class Sparrow(FlyingBird):
    pass

class Ostrich(Bird):
    pass
```



## Interface Segregation Principle (I):
A class should not be forced to implement the interfaces it does not use
### Sample Code
```python
# Bad Example
class Worker:
    def eat(self):
        pass
    def work(self):
        pass

# Good Example
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass

class Human(Workable, Eatable):
    def work(self):
        print("Working")
    def eat(self):
        print("Eating")

class Robot(Workable):
    def work(self):
        print("Robot is working")
```



# Dependency Inversion Principle (D):
High-level moudles should not be depend on low-level modules. Both should depend on abstractions
```python
# Bad Example
class Keyboard:
    def type(self):
        print("Typing")

class Computer:
    def __init__(self):
        self.keyboard = Keyboard()

# Good Example
class InputDevice:
    def type(self):
        pass

class Keyboard(InputDevice):
    def type(self):
        print("Typing")

class Computer:
    def __init__(self, device):
        self.device = device

    def start_typing(self):
        self.device.type()

keyboard = Keyboard()
computer = Computer(keyboard)
computer.start_typing()
```

These principles helps devlopers with software that is:
- Easier to maintain
- Easier to test
- More reusable
- More scalable
- Less tightly coupled 