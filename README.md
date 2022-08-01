# python_OOP
Python Object-Oriented Tutorials. In this series, we will be learning how to create classes in Python, and also the best practices for working with these classes. We will go over class/instance variables, inheritance, getters/setters, and much more.
Reference:```link https://www.youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc```

fore create class in python :
```python
class Employee:

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

emp_1 = Employee('Corey', 'Schafer', 50000)
emp_2 = Employee('Test', 'Employee', 60000)

```
