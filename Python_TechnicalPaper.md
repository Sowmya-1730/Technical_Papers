# Python Cheatsheet


# Array methods
An array is a collection of same data type values. These elements are stored at contiguous memory location and elements can be accessed through index.
- Adding and removing elements in array
    - append(x) --> This method will append a new value x at the end of the array (arr.append(10))
    - extend(iterable) --> This will append items from iterable objects like list,set,tuple to the end of array (arr.extend(list_example))
    - insert(i, x) --> This will insert the value x at the index position i (arr.insert(2,10))
    - pop([i]) --> This method will help us to remove the value at index i. If we didn't give the index then it will remove last element of array (arr.pop(), arr.pop(2))
    - remove(x) --> This method will help us to remove the first occurence of value x in the array (arr.remove(10))

- Information and Utitliy methods
    - buffer_info() --> This method will give the address and length of the array (arr.buffer_info())
    - count(x) --> This method will count the occurences of value x in the array (arr.count(10))
    - index(x [, start[, stop]]) --> This method will help us to find the index position of value x and we can give ranges to search for (arr.index(10,1,5))

- Manipulating Array elements
    - reverse() --> It will reverse the order of items in the array (arr.reverse())
    - byteswap() --> It reverses the byte order of elements (arr.byteswap())

- Conversion methods
    - frombytes(buffer) --> It reads data from bytes object or bytearray to append to array existing array (arr.frombytes(b'\x04\x00\x00\x00'))
    - tobytes() --> Converts the array to bytes representation (arr.tobytes())
    - fromfile(f, n) --> It reads the n number of items from file and append to the array (arr.fromfile(file_name, 6))
    - tofile(n) --> It write all n number of items to the file (arr.tofile(var)) (var = [1,2,3,4,5])
    - tolist() --> It converts the array to list iterable object (arr.tolist())
    - fromunicode(s) --> Extends the array with data from the given unicode string. The string should contains code 'u'
    - tounicode() --> Converts the array to unicode string



# String methods
String is a immutable sequence of unicode characters. We cannot change the string once it was created.
- Case Conversion methods
    - capitalize() --> This method will help us to capitalize the first letter of string (s.capitalize())
    - casefold() --> It converts upper case letters to lower case and vice versa and it will work on UNICODE characters also (s.casefold())
    - lower() --> Converts entire string into lower case letters (s.lower())
    - swapcase() --> Converts upper to lower and lower to upper cases (s.swapcase())
    - title() --> Converts the string to title case where every first character in each word will be converted to upper case and remaining are lower case (s.title())
    - upper() --> Converts the entire string into upper case letters (s.upper())

- Alignment methods
    - center(width, fillchar) --> For this method we will give width means how much length of the string we want and by that if we have empty spaces we will fill it with by give character in fillchar option) (s.center(10,'-'))
    - ljust(width[,fillchar]) -->  It returns left-justified string and if we want to fill it we can give character for that to fill empty spaces (s.ljust(12,'?'))
    - rjust(width[,fillchar]) --> It returns right-justified string and if we want to fill it we can give character for that to fill empty spaces (s.rjust(12,'?'))
    - expandtabs(tabsize = 8) --> Expand the tab in string to multiple spaces; defualt value is 8 (s.expandtabs(10))
    - zfill(width) --> It returns original string with left-padded and fill it with zerors (s.zfill(10))

- Split and Join methods
    - lstrip() --> It removes the left side empty spaces (s.lstrip())
    - rstrip() --> It removes all right side trailing empty spaces (s.rstrip())
    - strip() --> It removes all leading and trailing empty spaces (s.strip())
    - rsplit() --> Splits the string from the end and return list of substrings (s.rsplit())
    - split() --> It will split the string based on the delimiter (s.split(' '))
    - splitlines() --> It will split the lines of string into list of lines and each line will become a single string (s.splitlines())
    - partition() --> It will separate the string in three string tuple at the first occurence of separator (s.partition())
    - rpartition() --> It will separate the string in three string tuple at last occurence of separator (s.rpartition())
    - join() --> It will concatenates the string representation of elements (s.join())
    - removeprefix() --> It will return the string after removing the prefix (s.removeprefix())
    - removesuffix() --> It will return the string after removing the suffix (s.removesuffix())

- Boolean string methods
    - isalnum() --> Returns True if string is combination of letters and numbers else False (s.isalnum())
    - isalpha() --> Returns True if all characters in string are letters else False (s.isalpha())
    - isdigit() --> Returns True if string contains only digits else False (s.isdigit())
    - islower() --> Returns True if all characters are in lower case else False (s.islower())
    - isnumeric() --> Returns True if unicode strings will only contains numeric characters else False (s.isnumeric())
    - isspace() --> Returns True if string contains only whitespaces else False (s.isspace())
    - istitle() --> Returns True if each string is properly title cased else False (s.istitle())
    - isupper() --> Returns True if entire string is in upper case else False (s.isupper())
    - isascii() --> Returns True if all the characters in the string are in ASCII character set (s.isascii())
    - isdecimal() --> Returns True if all the characters are decimal characters (s.isdecimal())
    - isidentifier() --> Returns True if string is valid identifier or not (s.isidentifier())
    - isprintable() --> Returns True if all the characters in the string is printable or not (s.isprintable())

- Find and Replace methods
    - count(sub, beg, end) --> It counts how many times the given substring is there in the string and it will check in range also if we given (s.count('hello',5,11))
    - find(sub, beg, end) --> It will find the substring in the string and also range if not there it will return -1 (s.find('hello',5,12))
    - index(sub, beg, end) --> It will find the substring in the string and also range if not there it will produce error (s.index('hello',5,10))
    - replace(old, new [,max]) --> It will replaces all occurences of old string with new or atmost if max is given (s.replace('hello','Hello',3))
    - rfind(sub, beg, end) --> It find the substring from right side of the string and also within the range if given it will return -1 if not found (s.rfind('hello',5,12))
    - rindex(sub, beg, end) --> It will find the substring from the right side of string and also within range and produces error if not found (s.rindex('world'))
    - startswith(sub, beg, end) --> Returns True if string is beginned with substring else False and it can also check within range (s.startswith('this',3,10))
    - endswith(suffix, beg, end) --> Returns True if string ends with substring else False and it can also check within range (s.endswith('world',27,30))

- Translation methods
    - maketrans() --> Returns a translation table to be used in translate function (s.maketrans(intab,outtab), intab="aeiou", outtab="12345", s="this is string example....wow!")
    - translate(table, deletechars="")  --> Translates string according to translation table str(256 chars), removing those in the del string. It is the sequel method of maketrans() in string module (s.translate()) 




# Objects and Object Oriented Programming
Object: An object is an instance of a class in Python. It represents the real-world entity with properties(data) and behaviors(methods). Objects are created using classes as blueptints. Object help implement Object-Oriented programming in python. 
```python
class Car:
    def __init__(self,brand):
        self.brand = brand
car1 = Car("Toyota")
```
Here, car1 is the object for Class Car.

Object-Oriented Programming: Object-Oriented Programming is a programming framework that organizes code using objects and classes. It helps in creating reusable, modular and maintainable programs. The four principles in OOPs are:
- Encapsulation: It is the process of combining data and methods into a single unit(class). Encapsulation helps in hiding internal implementation details from users. Data is usually controlled using getter and setter methods.
```python
class Student:
    def __init__(self):
        self.__marks = 80
    def show_marks(self):
        print(self.__marks)

s = Student()
s.show_marks()
```
- Polymorphism: Polymorphism means "many forms". It allows the same method or function name to behave differently depending on the object or context. By Polymorphism, the code will improves by flexibility and extensibility in programs.
```python
class Dog:
    def sound(self):
        print("Dog barks")

class Cat:
    def sound(self):
        print("Cat meows")

d = Dog()
c = Cat()

d.sound()
c.sound()
```
- Abstraction: Abstraction hides unnecessary implementation details and shows only essential features to the user. It helps reduce the complexity in large applications. Users interact with only relevant functionalities without knowing the logic.
```python
from abc import ABC, abstractmethod

class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):

    def sound(self):
        print("Dog barks")

d = Dog()
d.sound()
```
- Inheritance: Inheritance allows one class to acquire properties and methods from another class. It will be called as parent and the class which takes inheritance from parent class will be called as child class. Child classes can add new features or modify inherited behaviour. It promotes code reusability and reduces redundancy.
```python
class Parent:
    def show(self):
        print("This is parent class")

class Child(Parent):
    pass

c = Child()
c.show()
```


# Decorators
Decorators are special functions used to modify or extend the behaviour of other functions or methods. They allow code reusage without changing the original function's source code. Decorators are commonly represented with '@' symbol in Python. Decorators improve code modularity and maintainability. Below is the syntax for Decorators.
```python
@decorator_name
def function_name():
    pass
```


# virtualenv
A virtual environement is an isolated Python environment used to manage project specific dependencies. It allows for different projects to use different package versions without conflicts. It help keep the global Python installation clean and organized.
- python3 -m venv venv (Create a virtual environment)
- source venv/bin/activate (To activate the virtual environment)
- deactivate (To deactivate the virtual environment)


# pip package manager
pip is the default package manager used in Python to install and manage external libraries and packages. It helps developers to easily download, update, and remove Python packages from the Python Package Index (PyPi)
- pip install package_name (To install python package)
- pip uninstall package_name (To remove python package)
- pip list (It will list out all installed python packages)
- pip freeze (Shows installed installed packages with versions)
- pip install -r requirements.txt (Install all dependencies from a requirement file)
- pip install --upgrade package_name (Updates a existing package)



# PEP-8 standards summary
PEP-8 is the official style guide for Python code. It helps developers write clean, readable and consistent programs. Most common points to remember are:
- Use 4 spaces for indentation consistently
- Avoid mixing tabs and spaces in code
- Limit code line to 79 characters
- Limit comments and docstrings to 72 characters
- Use blank lines properly to separate functions and classes
- Write each import statement on a separate line
- Organize imports into standard, third party, and local imports
- Use snake_case for variables and function names
- Use CamelCase for classe names
- Use UPPPER_CASE for constants
- Prefix internal or private variables with an underscore
- Add spaces around operators and after commas
- Avoid unnecessary whitespace in expressions and statements
- Write meaningful and descriptive variable names
- Use comments only when necessary and keep them clear
- Add docstrings for modules, classes and functions
- Avoid overly complex or deeply nested code
- Use specific exception handling instead of generic except blocks
- Keep functions small and focused on a single task
- Use is for comparisons with None
- Use == for value comparisons
- Prefer readable list comprehension over complex loops when appropriate
- Use trailing commas in multiline collections for cleaner formatting
- Name files and modules using lowercase letters with underscores
- Maintain consistent coding style throughout the project
- Follow readability and simplicity as primary coding principles
- Avoid redundant code and unnecessary comments
- Use proper spacing between functions, classes and code blocks
- Write code that is easy to maintain and collaborate on
- Use tools like pylint, flake8, black and autopep8 to enforce PEP 8 standards.


##  References

- Python Official Documentation: https://docs.python.org/3/
- PEP 8 Style Guide: https://peps.python.org/pep-0008/
- Python Package Index (PyPI): https://pypi.org/
- Virtual Environment Documentation: https://docs.python.org/3/library/venv.html
- Tutorials Point Tutorial: https://www.tutorialspoint.com/python/index.html



































