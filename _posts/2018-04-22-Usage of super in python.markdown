---
layout: post
title:  "Usage of super in python"
date:   2018-04-22 9:22:00
categories: python
tags: python
---

* content
{:toc}

## Usage of super in python

Super(from python2.2) can call method of parent using super(parentclass, self).parentmethod(), self is object of child class, super can automatically transform object of child class to object of parent class. Keep in mind, super is a class, not a method, once called, the `__init__` method of super returns an object of parent class. See sample code below:





```python
class A:
    def __init__(self):
        print("Enter A")
        print("Leave A")

class B(A):
    def __init__(self):
        print("Enter B")
        super(B, self).__init__()
        print("Leave B")

class C(A):
    def __init__(self):
        print("Enter C")
        super(C, self).__init__()
        print("Leave C")

class D(B, C):
    def __init__(self):
        print("Enter D")
        super(D, self).__init__()
        print("Leave D")

d = D()
``` 

### Output
>*    Enter D
>*    Enter B
>*    Enter C
>*    Enter A
>*    Leave A
>*    Leave C
>*    Leave B
>*    Leave D

Let's use parentclass.method instead, see code below:

```python
class A:
    def __init__(self):
        print("Enter A")
        print("Leave A")

class B(A):
    def __init__(self):
        print("Enter B")
        A.__init__(self)
        print("Leave B")

class C(A):
    def __init__(self):
        print("Enter C")
        A.__init__(self)
        print("Leave C")

class D(B, C):
    def __init__(self):
        print("Enter D")
        super(D, self).__init__()
        print("Leave D")

d = D()
```

### Output

>*    Enter D
>*    Enter B
>*    Enter A
>*    Leave A
>*    Leave B
>*    Leave D

Why? Class C has benn ignored though D is inherited from B and C, let's see the tree of relationship.


 >   object
       |
       A
      / \
     B   C
      \ /
       D

**Conclusion1:**
We can consider class which contains super() in the heritage tree as a valid node(A is a valid node). 

* If B, C, D has super(), all nodes are valid nodes, the visit sequence is D->B->C->A

* If D, B has super(), D, B, A are valid nodes, the visit sequence is D->B->A

I think you have found the rule, python implements BFS on the valid nodes. Actually, I didn't find any documentations about this, however, in python source code, we found[^reference]:

```c
 static PyObject *
 super_getattro(PyObject *self, PyObject *name)
 {
  superobject *su = (superobject *)self;
  int skip = su->obj_type == NULL;
  ……
  if (!skip) {
   PyObject *mro, *res, *tmp, *dict;
   PyTypeObject *starttype;
   descrgetfunc f;
   int i, n;

   starttype = su->obj_type;  // 获得搜索的起点：super对象的obj_type
   mro = starttype->tp_mro;  // 获得类的mro
   ……
   for (i = 0; i < n; i++) {  // 搜索mro中，定位mro中的type
    if ((PyObject *)(su->type) == PyTuple_GET_ITEM(mro, i))
     break;
   }
   i++;       // 切换到mro中的下一个类
   res = NULL;
   for (; i < n; i++) {   // 在mro以后的各个命名空间中搜索指定名字
    tmp = PyTuple_GET_ITEM(mro, i);
    if (PyType_Check(tmp))
     dict = ((PyTypeObject *)tmp)->tp_dict;
    else if (PyClass_Check(tmp))
     dict = ((PyClassObject *)tmp)->cl_dict;
    else
     continue;
    res = PyDict_GetItem(dict, name);
    if (res != NULL) {
     Py_INCREF(res);
     f = res->ob_type->tp_descr_get;
     if (f != NULL) {
      tmp = f(res, su->obj,
       (PyObject *)starttype);
      Py_DECREF(res);
      res = tmp;
     }
     return res;
    }
   }
  }
  return PyObject_GenericGetAttr(self, name);
 }
```

From C code above, we can find PyObject *mro records the sequence of all root classs. 

**Conclusion2:**

* Super() is an unbound type to call parent method, if we need to modify parent class names frequently, it's not recommended to use bound type(parentclass.method) because we need to travasal the child class to modify all parent class names.
* Combining unbound type and bound type in a child class is danger because it may cause leak of parent classes.

[^reference]: 参考博客[1]
[1]: https://blog.csdn.net/johnsonguo/article/details/585193