---
layout: post
title:  "Some difference methods in python"
date:   2018-08-21 22:29:00
categories: python
tags: python
---

* content
{:toc}

## 主要罗列了Python中static方法 class方法 object方法的区别 以及他们与C++等静态语言不一样的地方

### Python Code

```python

import time

class SuperClass:
    superpower_list = []
    superpower_var = 1

    def __init__(self, name):
        self.name = name

    def add_superpower_list(self, power):
        self.superpower_list.append(power)

    def change_superpower_var(self, power):
        self.superpower_var = power

    @staticmethod
    def superpower_static_method(var1, var2):
        return var1 + var2

    @classmethod
    def superpower_class_method(cls, var):
        cls.superpower_var = var

#Initialize
print("Initialize...")
time.sleep(2)
foo = SuperClass('foo')
print("foo.name:")
print(foo.name)

#Test if list can be changed by instance
print("foo.add_superpower_list('fly')")
foo.add_superpower_list('fly')
print(foo.superpower_list)
print(SuperClass.superpower_list)

print("foo.superpower_list.append('fly1')")
foo.superpower_list.append('fly1')
print(foo.superpower_list)
print(SuperClass.superpower_list)

print("SuperClass.superpower_list.append('fly2')")
SuperClass.superpower_list.append('fly2')
print(foo.superpower_list)
print(SuperClass.superpower_list)

#Test if variable can be changed by instance
print("foo.change_superpower_var(1)")
foo.change_superpower_var(1)
print(foo.superpower_var)
print(SuperClass.superpower_var)

print("foo.superpower_var = 2")
foo.superpower_var = 2
print(foo.superpower_var)
print(SuperClass.superpower_var)

print("SuperClass.superpower_var = 3")
SuperClass.superpower_var = 3
print(foo.superpower_var)
print(SuperClass.superpower_var)

#Test if variable can be changed by cls method
print("foo.superpower_class_method(4)")
foo.superpower_class_method(4)
print(foo.superpower_var)
print(SuperClass.superpower_var)

print("SuperClass.superpower_class_method(5)")
SuperClass.superpower_class_method(5)
print(foo.superpower_var)
print(SuperClass.superpower_var)

#Compare id of foo.mutable and SuperClass.mutable, foo.immutable and SuperClass.immutable
print("id(SuperClass.superpower_list)")
print(id(SuperClass.superpower_list))
print(hex(id(SuperClass.superpower_list)))
print("id(foo.superpower_list)")
print(id(foo.superpower_list))
print(hex(id(foo.superpower_list)))

print("id(SuperClass.superpower_var)")
print(id(SuperClass.superpower_var))
print(hex(id(SuperClass.superpower_var)))
print("id(foo.superpower_var)")
print(id(foo.superpower_var))
print(hex(id(foo.superpower_var)))

#Test static method
print("foo.superpower_static_method(1, 2)")
print(foo.superpower_static_method(1, 2))
print("SuperClass.superpower_static_method(2, 3)")
print(SuperClass.superpower_static_method(2, 3))

SuperClass.a = 3
print(SuperClass.a)

```