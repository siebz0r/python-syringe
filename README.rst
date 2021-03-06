=======
Syringe
=======

.. image:: https://travis-ci.org/remcohaszing/grunt-angular-templatecache.png?branch=master
   :target: https://travis-ci.org/remcohaszing/python-audiolayer

A simple dependency injection library.


Usage example
=============

First decorate a class with ``@provides('a lookup name')``.

>>> import syringe
>>>
>>> @syringe.provides('cure')
... class Syrup:
...     def drink(self, person):
...         print('Nom nom')
...         person.health = 100
...

Instantiate it. Note that it is not possible to instanciate another instance of
a class decorated with the name ``cure``.

>>> syrup = Syrup()

Next inject it in another class using ``inject('a lookup name')``.

>>> class Person:
...     cure = syringe.inject('cure')
...
...     def drink_medicine(self):
...         self.cure.drink(self)
...

When an instance of the ``Person`` class is created, the value of the injecte name
is the instance of the provided and instantiated class.

>>> person = Person()
>>> person.health = 20
>>> assert person.cure == syrup
>>> person.drink_medicine()
Nom nom
>>> assert person.health == 100


Mocking
-------

A mock instance can be inserted using ``syringe.mock('a lookup name')``

>>> try:
...     from unittest import mock
... except:
...     import mock
...
>>> m = syringe.mock('cure')
>>> person.drink_medicine()
>>> m.drink.assert_called_once_with(person)


Installing
==========

The package can be installed from the cheese shop by typing::

    pip install syringe
