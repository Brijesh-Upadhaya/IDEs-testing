---
layout: episode
title: "Motivation"
teaching: 10
exercises: 0
questions:
  - "Why should we write tests?"
  - "Why does code complexity and good design practices matter?"
  - "What does an IDE bring to software development?"
objectives:
  - "Discuss the advantages of writing and maintaining tests in research software."
  - "Discuss the learning curve - efficiency tradeoff in using IDEs"
keypoints:
  - "Do not trust software when its tests do not cover its claimed capabilities
     (test coverage) and when its tests do not pass or if there are no tests at all
     or if the tests are never run."
  - "The more you write code, the more time you can save by learning to use an
    IDE"
---

## Introduction

In CodeRefinery discussions everyone agreed that three things should be
trained:

* modular code development and good code design principles
* unit testing, especially the practice of automatically running tests for
  each commit called Continuous Integration
* using IDEs to save time in common software development tasks

Modular code development is best taught via examples. However the fact that
examples must be in a real-world programming language makes it difficult to
make good, generic exercises. A discussion about code development practices in
pseudocode or without examples is often a bit wanting.

Unit testing  code is always important, but doing rapid iterative exercises
using just a text-based editor is not always straightforward. An IDE makes
writing tests and debugging tests considerably faster.

Finally simply learning to use all the bells and whistles of an IDE with
isolated examples does not really motivate the individual.

This session is an attempt to combine the three topics. The concepts covered
in each part are necessarily a bit lighter, but hopefully this approach
concretizes the facts that:

* good tests are necessary
* complexity matters
* an IDE can be a powerful enabler in typical programming workflows

---

## Testing

In software tests, expected results are compared with observed results in order
to establish accuracy:

```python
def get_bmi(mass_kg, height_m):
    """
    Calculates the body mass index.
    """
    return mass_kg/(height_m**2)


def test_get_bmi():
    bmi = get_bmi(mass_kg=90.0, height_m=1.91)
    expected_result = 24.670376
    assert abs(bmi - expected_result) < 1.0e-6
```

`assert` translates to English as "make sure that".

---
##  What is an IDE?

keyword: **INTEGRATED**


**The visual representation of an IDE is close to:**

<img src="{{site.baseurl}}/img/10-wave-fanned-black-oxide.jpg"
style="width:45%"><img
src="{{site.baseurl}}/img/10-wave-closed-black-oxide.jpg" style="width:45%">

## What is modular code?

Writing code is a process of creating levels of abstraction. Engineers with
systems background can simply think that they should create their code as a
number of interconnected, but mostly isolated *systems* that only talk to each
other via well-defined *interfaces*. In programming, these interfaces are
often APIs.

What is a system? A system is an entity that can be easily told apart from
it's environment. In biology, a cell is an example of a system. It as a
well-defined border in the cellular wall and they ways in which a cell
interacts with it's environment are (thought to be) known.  An individual
organ is an example of a system on another level. In scientific experiments
the experiment design is usually designed to be a system that is mostly
isolated from it's environment. Typically something from the environment will
start and stop the experiment and observe the results, but otherwise the
environment shouldn't affect the test.

Learning modular code design is a long road and the session is cramped, so we
will limit ourselves to mentioning modular code design concepts every now and
then.
