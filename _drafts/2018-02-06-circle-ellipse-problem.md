---
title : "I solved the circle-ellipse problem !?"
layout: post
---

Ok the title is clickbait. I did not. But I want to address my thoughts on the
subject.

The circle-ellipse or square-rectangle problem shows the limit of the Oriented-
Object paradigm and particularly the limit of inheritance.

The idea behind inheritance is to re-use code, creating new classes built upon
existing classes while maintaining the same behaviour.

The last point is important and known as Liskov Substitution Principle :

> Let q(x) be a property provable about objects x of type T.
> Then q(y) should be provable for objects y of type S
> where S is a subtype of T.

Concretly, it means that any methods/function applied to objects x can be
applied to any object y without altering any of the desirable properties of
that program.

For example, if we define the classes Vehicles and Cars :

	class Vehicles{
		void drive();
	}
	class Cars:Vehicles{
	}

Whether I use

	Vehicles.drive();

or

	Cars.drive();

it will work.

## But sometimes ...

Sometimes, we find a property of inheritance :

	A square is a rectangle
	A circle is an ellipse

and we start thinking. A square is a special case of rectangle, so rectangles 
can be substitute by squares and it should work.

No, it does not, if we use the `getHeight()` method on a square, it should fail
, because squares don't have a height.

What if we think about it, the other way. A rectangle is an extension of a
square. We can add attributes and methods to the class Rectangle, but we
definitely can't replace squares by rectangles.

Actually, both assumptions "a square is a rectangle" and "a rectangle extends a
square" are wrong. A square is not a rectangle.

## So how do I do ?

Just don't.

Square, rectangle, circle, ellipse are different.

# Deal with it

## bibliography

* https://en.wikipedia.org/wiki/Circle-ellipse_problem
* http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.39.1223
