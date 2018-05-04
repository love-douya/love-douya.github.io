---
layout: post
title: "Usage of brace-enclosed initializer list in struct and class in C++"
date: 2018-04-30 19:50
categories: C++
tags: C++
---

* content
{:toc}

## Usage of brace-enclosed initializer list in struct and class in C++

We know `struct` is a constructor in C language while `class` is based on `struct` in C++. However, that doesn't mean `struct` is discarded in C++, inversely, it has been given some new characters in C++, (e.g.:struct can be inherited from struct or class, we can declare public or private variable and function in struct , we can declare constructor and destructor in struct, we can also declare template for struct(compile polymorphism), ...). Based on my experience, the only difference between `struct` and `class` is in `class` we can declare virtual function(runtime polymorphism) while in `struct` we can't. OK, it's not today's point. Today we discuss about the {}. To make explanation be concise Let's see sample below:




### Sample Code1
```c++
#include <iostream>
using namespace std;

struct A{
public:
    int number = 1;
    const char* symbol = "b"; 
};

int main(){
    A pp = {2, "a"};
//Tip: << is an overloaded operator which returns an          object so that we can use <<A<<B<< ... <<C<<D sequencely.
    cout << pp.number << endl << pp.symbol << endl;
}
```
### Output1


>* pp.number:2
>* pp.symbol:a

### Sample Code2
```c++
#include <iostream>
using namespace std;

struct A{
public:
    int number = 1;
private:
    const char* symbol = "b"; 
};

int main(){
    A pp = {2, "a"};
    cout << pp.number << endl << pp.symbol << endl;
}
```
### Output2


>* error: could not convert '{2, "a"}' from '<brace-enclosed initializer list>' to 'A'
>* error: 'const char*A::symbol' is private within this context
>* note: declared private here

From results above, we know variable in struct can be initialized by {} but only public variable can be.Let's modify struct A:

### Sample Code3
```c++
#include <iostream>
using namespace std;

class A{
public:
    A(){};
    virtual ~A(){};
    int number = 1;
    const char* symbol = "b"; 
};

int main(){
    A pp = {2, "a"};
    cout << pp.number << endl << pp.symbol << endl;
}
```
### Output3

>* error: could not convert '{2, "a"}' from '<brace-enclosed initializer list>' to 'A'

From result above, we know if we has defined a constructor in struct(or class), {} can not be used because C++ complier will force us to initialize varible in the constructor.

> **Conclusion**: {} can be used in both struct and class, but only can be used to initialize public variable. In addition, if we have declared a constructor, we can't use {}. Sometimes it's so simple and convinient, right?




