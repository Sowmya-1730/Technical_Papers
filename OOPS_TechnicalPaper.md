# Object-Oriented Programming (OOP) in Python

Object-Oriented Programming (OOP) is a programming framework that organizes code using classes and objects. It helps in creating reusable, modular, and scalable applications. In Python, OOP allows developers to model real-world entities with properties and behaviors.

## Four Main Principles of OOP

### 1. Encapsulation

Encapsulation is the process of combining data and methods into a single unit called a class. It restricts direct access to data and protects it from accidental modification. They can only be accessed through the methods within the same class.

#### Example

```python
class Student:
   def __init__(self, name="Rajaram", marks=50):
      self.name = name
      self.marks = marks

s1 = Student()
s2 = Student("Bharat", 25)

print ("Name: {} marks: {}".format(s1.name, s2.marks))
print ("Name: {} marks: {}".format(s2.name, s2.marks))
```

---

### 2. Inheritance

Inheritance allows one class to acquire the properties and methods of another class. It promotes code reusability and reduces redundancy. The class that inherited will be called as Child class and the class which allowed for inheritance will be called as Parent class. There are five types in Inheritance:
- Single Inheritance - This is the simplest form of inheritance where a child class inherits attributes and methods from only one parent class.
- Multiple Inheritance - Multiple inheritance in Python allows you to construct a class based on more than one parent classes. The Child class thus inherits the attributes and method from all parents. The child can override methods inherited from any parent.
- Multilevel Inheritance - In multilevel inheritance, a class is derived from another derived class. 
- Hybrid Inheritance - Combination of two or mroe inheritances
- Hierarichal Inheritance - This type of inheritance contains multiple derived classes that are inherited from a single base class. 

#### Example

```python
# Parent class
class Parent: 
   def parentMethod(self):
      print ("Calling parent method")

# Child class
class Child(Parent): 
   def childMethod(self):
      print ("Calling child method")

c = Child()  
c.childMethod() 
c.parentMethod() 
```

---

### 3. Polymorphism

Polymorphism allows methods with the same name to behave differently based on the object calling them. If a method in a parent class is overridden with different business logic in its different child classes, the base class method is a polymorphic method.

### Ways to implementing Polymorphism in Python
- Duck Typing
- Operator Overloading
- Method overloading
- Method overriding

#### Duck Typing
Duck typing is a concept where the type or class of an object is less important than the methods it defines. Using this concept, you can call any method on an object without checking its type, as long as the method exists.

#### Example
```python
class Duck:
   def sound(self):
      return "Quack, quack!"

class AnotherBird:
   def sound(self):
      return "I'm similar to a duck!"

def makeSound(duck):
   print(duck.sound())

duck = Duck()
anotherBird = AnotherBird()
makeSound(duck)   
makeSound(anotherBird) 
```

##### Operator Overloading
Suppose you have created a Vector class to represent two-dimensional vectors, what happens when you use the plus operator to add them? Most likely Python will yell at you.

You could, however, define the __add__ method in your class to perform vector addition and then the plus operator would behave as per expectation
#### Example
```python
class Vector:
   def __init__(self, a, b):
      self.a = a
      self.b = b

   def __str__(self):
      return 'Vector (%d, %d)' % (self.a, self.b)
   
   def __add__(self,other):
      return Vector(self.a + other.a, self.b + other.b)

v1 = Vector(2,10)
v2 = Vector(5,-2)
print (v1 + v2)
```

##### Method Overloading
When a class contains two or more methods with the same name but different number of parameters then this can be termed as method overloading.
#### Example
```python
def add(*nums):
   return sum(nums)

result1 = add(10, 25)
result2 = add(10, 25, 35)

print(result1)  
print(result2) 
```

##### Method overriding
In method overriding, a method defined inside a subclass has the same name as a method in its superclass but implements a different functionality.
#### Example
```python
from abc import ABC, abstractmethod
class shape(ABC):
   @abstractmethod
   def draw(self):
      "Abstract method"
      return

class circle(shape):
   def draw(self):
      super().draw()
      print ("Draw a circle")
      return

class rectangle(shape):
   def draw(self):
      super().draw()
      print ("Draw a rectangle")
      return

shapes = [circle(), rectangle()]
for shape in shapes:
   shp.draw()
```

---

### 4. Abstraction

Abstraction hides implementation details and shows only the essential features to the user.

#### Example

```python
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass

class Square(Shape):

    def area(self):
        return 25

s = Square()
print(s.area())
```
