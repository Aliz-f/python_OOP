# python_OOP
Python Object-Oriented Tutorials.

In this series, we will be learning how to create classes in Python, and also the best practices for working with these classes. We will go over class/instance variables, inheritance, getters/setters, and much more.

Reference:```https://www.youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc```

For create class in python :
```python
class Employee:

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay
```

Regular methods automatically pass the instance as first argument, with ```self```: 
```python
    def fullname(self):
        return '{} {}'.format(self.first, self.last)
```
Add class variable, we can use it as variable for each instance or class method:
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

Classmethods automatically pass the class as first argument, with ```cls```:
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

# Inheritance - Creating Subclasses
parent class :
```python
class Employee:

    raise_amt = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)
```

create instance from Employee class:
```python

dev_1 = Employee('Corey', 'Schafer', 50000)
dev_2 = Employee('Test', 'Employee', 60000)

print(dev_1.email)
print(dev_2.email)

```
Child class ```Developer```: 
```python
class Developer(Employee):
    raise_amt = 1.10

    def __init__(self, first, last, pay, prog_lang):
        super().__init__(first, last, pay)
        self.prog_lang = prog_lang
```

create instance from ```Developer``` class:
```python
dev_1 = Developer('Corey', 'Schafer', 50000, 'Python')
dev_2 = Developer('Test', 'Employee', 60000, 'Java')

print(issubclass(Developer, Employee))
print(isinstance(dev_1, Developer))
print(isinstance(dev_1, Employee))
```
Child Class ```Manager```:
```python
class Manager(Employee):

    def __init__(self, first, last, pay, employees=None):
        super().__init__(first, last, pay)
        if employees is None:
            self.employees = []
        else:
            self.employees = employees

    def add_emp(self, emp):
        if emp not in self.employees:
            self.employees.append(emp)

    def remove_emp(self, emp):
        if emp in self.employees:
            self.employees.remove(emp)

    def print_emps(self):
        for emp in self.employees:
            print('-->', emp.fullname())
```
Create instance from ```Manager``` class:
```python
mgr_1 = Manager('Sue', 'Smith', 90000, [dev_1])

print(mgr_1.email)

mgr_1.add_emp(dev_2)
mgr_1.remove_emp(dev_2)

mgr_1.print_emps()

print(issubclass(Manager, Employee))
print(isinstance(mgr_1, Developer))
print(isinstance(mgr_1, Employee))
print(isinstance(mgr_1, Manager))
```

# Dunder methods
These methods allow us to emulate built-in types or implement operator overloading. These can be extremely powerful if used correctly.

Reference : ```https://docs.python.org/3/reference/datamodel.html#special-method-names```

```Employee``` class :
```python
class Employee:

    raise_amt = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)

    def __repr__(self):
        return "Employee('{}', '{}', {})".format(self.first, self.last, self.pay)

    def __str__(self):
        return '{} - {}'.format(self.fullname(), self.email)

    def __add__(self, other):
        return self.pay + other.pay

    def __len__(self):
        return len(self.fullname())
```
create instance from ```Employee``` and use dunder:

```python
emp_1 = Employee('Corey', 'Schafer', 50000)
emp_2 = Employee('Test', 'Employee', 60000)

print(emp_1.__str__)
print(emp_2.__repr__)
print(emp_1 + emp_2)
print(len(emp_1))

```
# Property Decorators - Getters, Setters, and Deleters
The property decorator allows us to define Class methods that we can access like attributes. 

```Employee``` class:
```python
class Employee:

    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def email(self):
        return '{}.{}@email.com'.format(self.first, self.last)

    @property
    def fullname(self):
        return '{} {}'.format(self.first, self.last)
    
    @fullname.setter
    def fullname(self, name):
        first, last = name.split(' ')
        self.first = first
        self.last = last
    
    @fullname.deleter
    def fullname(self):
        print('Delete Name!')
        self.first = None
        self.last = None

```
create instance for ```Employee```:
```python
emp_1 = Employee('John', 'Smith')
emp_1.fullname = "Corey Schafer"

print(emp_1.first)
print(emp_1.email)
print(emp_1.fullname)

del emp_1.fullname
```
