# python_OOP
Python Object-Oriented Tutorials. 
In this series, we will be learning how to create classes in Python, and also the best practices for working with these classes. We will go over class/instance variables, inheritance, getters/setters, and much more.

Reference:```https://www.youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc```

for create class in python :
```python
class Employee:

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay
```

regular methods automatically pass the instance as first argument, with ```self```: 
```python
    def fullname(self):
        return '{} {}'.format(self.first, self.last)
```
add class variable, we can use it as variable for each instance or class method:
```python
class Employee:

    num_of_emps = 0
    raise_amt = 1.04
    .
    .
    .
    def __init__(self, first, last, pay):
        .
        .
        .
        Employee.num_of_emps += 1
    
    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)
        #self.pay = int(self.pay * Employee.raise_amt)
        
```

classmethods automatically pass the class as first argument, with ```cls```:
```python
    @classmethod
    def set_raise_amt(cls, amount):
        cls.raise_amt = amount

    @classmethod
    def from_string(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, pay)
```
static method don't pass anything:
```python
    @staticmethod
    def is_workday(day):
        if day.weekday() == 5 or day.weekday() == 6:
            return False
        return True
```

for crate instance from class:
```python
emp_1 = Employee('Corey', 'Schafer', 50000)
emp_2 = Employee('Test', 'Employee', 60000)

Employee.set_raise_amt(1.05)

print(Employee.raise_amt)
print(emp_1.raise_amt)
print(emp_2.raise_amt)

emp_str_1 = 'John-Doe-70000'
emp_str_2 = 'Steve-Smith-30000'
emp_str_3 = 'Jane-Doe-90000'

first, last, pay = emp_str_1.split('-')

#new_emp_1 = Employee(first, last, pay)
new_emp_1 = Employee.from_string(emp_str_1)

print(new_emp_1.email)
print(new_emp_1.pay)

import datetime
my_date = datetime.date(2016, 7, 11)

print(Employee.is_workday(my_date))
```
