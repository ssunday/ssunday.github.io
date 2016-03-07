---
title: The Five solid SOLID Principles
description: A summary of what the five SOLID principles are
date: 10/3/2016
---
**S**:
* A class or method should do one thing--they should have one responsibility that they deal with.
* Tips: if, to describe it, you say AND, it probably isn’t following SRP.
* A class called Light switch should be able to go from on to off. It shouldn’t be able to change the bulbs or control electricity.
* Based on change. It should exist as a reason for change.
* Method should return something or modify something, not both.

**O**:
* Programs can be expanded upon, but their current functionality should not be modified. There is room for additions/improvements, but no changes in what it does.

**L**:
* The child should be able to be substituted for its parent to the same effect. Or, in a more verbose fashion, sub-types can function as their parent types.
* A subclass should do the same things as the parent, and if switched, the program will not explode.
* Both Dog and Poodle can bark. By substituting poodle for dog, anything that uses bark will not fail. Of course, output changes, but the function is the same.

**I**:
* Interfaces should be specific to the need and not have extraneous features that aren’t being used.
* Basically to enforce decoupling to allow for more change along the road.

**D**:
* Depend on abstractions, high-level concepts associated with the problem rather than specifics or ‘concretions.’
