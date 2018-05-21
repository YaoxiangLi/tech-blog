---
title: Python metaclasses
categories: Python
abbrlink: 49908
date: 2014-01-03 12:36:37
tags:
    - Python
    - Metaclass
---

## Classes as objects

Object-oriented programming (OOP) is a programming paradigm based on the concept of "objects", which may encapsulate data, in the form of fields, often known as attributes; and code, in the form of procedures, often known as methods.

Class is the blue print of objects, and it describes the common attributes and methods. An object is a instance of a class.

For example:

```python
class ObjectCreator(object):
    pass

my_object = ObjectCreator()
my_object

<__main__.ObjectCreator object at 0x7fda8be489b0>
```

However, what gonna happen if we run the following code?

```python
print(ObjectCreator)
<class '__main__.ObjectCreator'>
```

This object (the class) is itself capable of creating objects (the instances), and this is why it's a class.

But still, it's an object, and therefore:

- you can assign it to a variable
- you can copy it
- you can add attributes to it
- you can pass it as a function parameter

## Creating classes dynamically

ObjectCreator as a class can be print out, and it self is a kind of object.

In some cases, we want to dynamicly create different kinds of class.

```python
def generate_cls(a, b):
    class Fake(object):
        def method_a(self, n):
            return n
    Fake.a = a
    Fake.b = b
    return Fake

class1 = generate_cls(1, 2)
class2 = generate_cls(2, 3)
ins1 = class1()
ins1.a, ins1.b, ins1.method_a(10)
ins2 = class2()
ins2.a, ins2.b, ins2.method_a(10)
```

There are some drawbacks for the procedure:

- Class name is not easy to modify
- When the attributes and methods rolling into a big number, it is hard to handle.

Here is a another way to do the job:

```python
def method_a(self, n):
    return n

ins = type('Fake', (), {'a': 1, 'b': 2, 'method_a': method_a})()

ins.a, ins.b, ins.method_a(10)
```

The **type** function can show you which type a object belongs to, and it has another useage, that is, create a class.

```python
type(1)
type('1')
type(ObjectCreator)
type(ObjectCreator())
```

**Type** it self is a function that takes descriptions of class as inputs and a class as output, which is a **metaclass**. So actually, **type** as a metaclass create every class. As we all know that in Python, everything, and I mean everything, is an object in Python. That includes ints, strings, functions and classes. All of them are objects. And all of them have been created from a class:

```python
age = 15

age.__class__

name = 'bob'

name.__class__

```

Now, what is the __class__ of any __class__ ?

```python
>>> age.__class__.__class__
<type 'type'>
>>> name.__class__.__class__
<type 'type'>
>>> foo.__class__.__class__
<type 'type'>
>>> b.__class__.__class__
<type 'type'>
```

So, a metaclass is just the stuff that creates class objects. You can call it a 'class factory' if you wish. Type is the built-in metaclass Python uses, but of course, you can create your own metaclass.

## The __metaclass__ attribute

You can add a __metaclass__ attribute when you write a class:

```python
class Foo(object):
    __metaclass__ = something...
    [...]
```

If you do so, Python will use the metaclass to create the class Foo.

You write class Foo(object) first, but the class object Foo is not created in memory yet.

Python will look for __metaclass__ in the class definition. If it finds it, it will use it to create the object class Foo. If it doesn't, it will use type to create the class.

When you do:

```python
class Foo(Bar):
    pass
```

Python does the following:

Is there a __metaclass__ attribute in Foo?

If yes, create in memory a class object (I said a class object, stay with me here), with the name Foo by using what is in __metaclass__.

If Python can't find __metaclass__, it will look for a __metaclass__ at the MODULE level, and try to do the same (but only for classes that don't inherit anything, basically old-style classes).

Then if it can't find any __metaclass__ at all, it will use the Bar's (the first parent) own metaclass (which might be the default type) to create the class object.

Be careful here that the __metaclass__ attribute will not be inherited, the metaclass of the parent (Bar.__class__) will be. If Bar used a __metaclass__ attribute that created Bar with type() (and not type.__new__()), the subclasses will not inherit that behavior.

Now the big question is, what can you put in __metaclass__ ?

The answer is: something that can create a class.

And what can create a class? type, or anything that subclasses or uses it.

## Custom metaclasses

The main purpose of a metaclass is to change the class automatically, when it's created.

You usually do this for APIs, where you want to create classes matching the current context.

Imagine a stupid example, where you decide that all classes in your module should have their attributes written in uppercase. There are several ways to do this, but one way is to set __metaclass__ at the module level.

This way, all classes of this module will be created using this metaclass, and we just have to tell the metaclass to turn all attributes to uppercase.

Luckily, __metaclass__ can actually be any callable, it doesn't need to be a formal class (I know, something with 'class' in its name doesn't need to be a class, go figure... but it's helpful).

So we will start with a simple example, by using a function.

```python
# the metaclass will automatically get passed the same argument
# that you usually pass to `type`
def upper_attr(future_class_name, future_class_parents, future_class_attr):
    """
      Return a class object, with the list of its attribute turned
      into uppercase.
    """

    # pick up any attribute that doesn't start with '__' and uppercase it
    uppercase_attr = {}
    for name, val in future_class_attr.items():
        if not name.startswith('__'):
            uppercase_attr[name.upper()] = val
        else:
            uppercase_attr[name] = val

    # let `type` do the class creation
    return type(future_class_name, future_class_parents, uppercase_attr)

__metaclass__ = upper_attr # this will affect all classes in the module

class Foo(): # global __metaclass__ won't work with "object" though
    # but we can define __metaclass__ here instead to affect only this class
    __metaclass__ = upper_attr
    # and this will work with "object" children
    bar = 'bip'

print(hasattr(Foo, 'bar'))
# Out: False
print(hasattr(Foo, 'BAR'))
# Out: True

f = Foo()
print(f.BAR)
# Out: 'bip'
```
