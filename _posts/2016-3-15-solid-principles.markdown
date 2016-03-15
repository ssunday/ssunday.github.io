---
title: The Five Solid SOLID Principles
description: A summary of what the five SOLID principles are
date: 15/3/2016
---

Just a collection of some wisdom/thoughts on each of the SOLID principles put forth by Uncle Bob. SOLID = Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion. Together they are the power team that help make clean code happen.

**S - Single Responsibility**:
* A class or method should do one thing--they should have one responsibility that they deal with.
* Separate responsibility so when alteration happens the code that needs to be changed is the only thing that is changed.
* If, to describe it, you say AND, it probably isn’t following SRP.
* Method should return something or modify something, not both.
* The name should describe exactly what it is doing or what it is describing.
* Methods should tend to be small, or else they are probably doing too many things and should be broken up. Same goes for classes and files

**O - Open/Closed**:
* Programs can be expanded upon, but their current functionality should not be modified.
* There is room for additions/improvements, but should be no changes in what it is/does.
* Core functionality should be static and consistent.
* Having it closed to modification reduces rippling effect on code that relies on it to act a certain way.
* But doesn’t remove the ability for future code to rely on methods that do not yet exist.

**L - Liskov Substitution**:

* A child should be able to be substituted for its parent to the same effect. Or, in a more verbose fashion, subtypes can function as their parent types.

* A subclass should do the same things as the parent, and if switched, the program will not explode.

* The functionality inherited should be present in some fashion and not conflict with the parent.

* From a more mathematical principle involving types and sub-types.

**I - Interface Segregation**:

* Interfaces should be specific to the need and not have extraneous features that aren’t being used.

* The client uses exactly what they need and should not have access to things that they do not need.

* Implement exactly what is needed by breaking each sector into its own piece and thus picking and choosing what matters.

* Sometimes things are not as similar as we think and we waste a lot by inheriting more than we should.

* Specialization is good as it can reduce waste by doing too much alteration on an existing template that really does not fit the specific needs.

**D - Dependency Inversion**:

* Depend on abstractions or high-level concepts associated with the problem rather than specifics or ‘concretions.’

* Less likely to change.

* Rely on the behavior expected rather than the implementation to arrive at that behavior.

* Bad Analogy: Know where point A and B are, don’t rely that you are taking a car there.


So yeah. Those are my thoughts on them right now. They may grow and harden into something more coherent and expansive, but here they are in all their fledgling glory.
