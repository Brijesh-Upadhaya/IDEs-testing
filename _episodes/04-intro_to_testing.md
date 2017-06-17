---
layout: episode
title: "Motivation"
teaching: 10
exercises: 0
questions:
  - "What are tests and how do they support writing software?"
objectives:
  - "Introduce basic concept of tests"
  - "Explain the gritty facts of writing tests"
keypoints:
  - "Testing is a
---


## Testing

To recap a text looks like the following

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

`assert` is English and means "make sure that".

Why are we not comparing directly all digits with the expected result?

---


## Tests make sure that expected functionality is preserved

- More robust code
- As projects grow, it becomes easier to break things without noticing immediately
- In particular for non-modular entangled projects (effects at distance)
- Testing helps detecting errors early:
  programming without constantly testing your changes will introduce errors
  and it is extremely time consuming to detect and fix them
- Interpreted dynamically typed imperative languages need to be tested
- So do compiled languages but the compiler catches at least some errors
- We publish scientific papers based on scientific code
- Scientific software cannot be called scientific unless it has been validated
  (taken from [Testing and Continuous Integration with Python](http://katyhuff.github.io/python-testing/))
- Testing is essential for research software because we care about
  reproducibility of scientific results and because derivative research and
  programs depend on research software


  "Program testing can be used to show the presence of bugs, but never to show their absence!" (Edsger W. Dijkstra)

  ""Be careful about using the following code - I’ve only proven that it works, I haven’t tested it." -Donald Knuth

---

### Simulations and analysis with untested software do not constitute science

"Before relying on a new experimental device, an experimental scientist always
establishes its accuracy. A new detector is calibrated when the scientist
observes its responses to known input signals. The results of this
calibration are compared against the expected response. An experimental
scientist would never conduct an experiment with uncalibrated detectors - that
would be unscientific. So too, simulations and analysis with untested
software do not constitute science."
(copied from [Testing and Continuous Integration with Python](http://katyhuff.github.io/python-testing/),
created by Kathryn Huff, see also the Testing chapter in
[Effective Computation In Physics](http://physics.codes) by Anthony Scopatz and Kathryn Huff)

---

## Tests help users of your code

- Users and computing center personnel may not be able to identify incorrect
  installation without automated testing (running a calculation and checking results
  with the naked eye is not automated testing)
- Users of your code publish papers based on results produced by your code
- Your peers need to be able to reproduce your (to be) published computational results
- The most likely person to use your code is *you* at some point in the
  future
- Forgetting what you did and why you did it sets you in the same position as
  a new developer

---

## Tests help developers of your code

- Satisfying instant visual feedback
- Avoid coding constipation
- Avoid "gold-plating" the code
- Tests make it possible to refactor the code
- Tests force you to think about the modularity of your code
- Code is unsustainable without runnable tests and becomes legacy software


---

## Tests facilitate external contributions

Tests can be good documentation of what the code is capable to do and how it is
supposed to be used since the tests are **documentation which is up to date by
definition**.

Easier for external developers to contribute to the project without breaking
your code.

Suiting up to modify untested code:

<img src="{{ site.baseurl }}/img/suit.jpg" style="width: 400px;"/>

Easier for you to accept contributions from others knowing that functionality
has been preserved.

---

## Tests help managing complexity

- Help to identify dependencies when modularizing and encapsulating code
- Unit tests sharpen and document interfaces
- Enable reuse and migration
- Faster coding: allows to make big changes quickly; refactoring
- You start with design; often leads to better design
- Well structured code is easy to test
- **Tests guide towards modular code structure**

Typical steps in creating a feature

#1 It works
#2 You had to change everything to make it testable but now the tests pass and
it works
#3 [time passes]
#4 You discover you can reuse part of the code with small modifications for
another feature
#5 The tests help you know you haven't broken old functionality in the
refactor

## Tests make it more difficult to add code smells

- Some things are difficult to test
- E.g. side-effects like printing things to stdout in the middle of a
  fucntion are typically cumbersome
- They are often cumbersome by design so that the extra effort would guide you
  to avoid side-effects where they do not belong and keep your code functional
  where it can be

#### Good code: pure and easy to test

```python
# function which computes the body mass index
def get_bmi(mass_kg, height_m):
    return mass_kg/(height_m**2)

# compute the body mass index
bmi = get_bmi(mass_kg=90.0, height_m=1.91))
```

#### Less good code: has side effects and is difficult to test

```python
mass_kg = 90.0
height_m = 1.91
bmi = 0.0

# function which computes the body mass index
def get_bmi():
    global bmi
    bmi = mass_kg/(height_m**2)
    print("computed a BMI of %d" % bmi)

# compute the body mass index
get_bmi()
```
# Terminology

## Defensive programming

Assume that mistakes will happen and introduce guards against them:
- Assertions
- Unit tests
- Regression tests

---

## How?

Imperfect tests run frequently are better than perfect tests which are never written

### Important

- Test frequently (each commit)
- Test automatically ([Travis CI](https://travis-ci.org))
- Test with numerical tolerance
- Think about code coverage ([Coveralls](https://coveralls.io))

---

## Unit tests

- Unit tests are functions ([Testing and Continuous Integration with Python](http://katyhuff.github.io/python-testing/))
- Test one unit: module or even single function
- Help to sharpen interfaces by identifying dependencies
- Speed up testing
- Good documentation of the capability and dependencies of a module
- In fact it is a documentation that is up to date by definition

---

## Integration tests

- Integration tests verify whether muliple modules are working well together ([Testing and Continuous Integration with Python](http://katyhuff.github.io/python-testing/))
- Like in a car assembly we have to test all components independently and also whether the components are working together when combined
- Unit tests can be used for testing independent components (e.g. engine, radiator, transmission) and integration tests to check if car is working overall
- Essential for having adequate testing
- An imperfect integration test is better than no integration test at all

---
## Test-driven development

- Write tests before writing code
- Very often we know the result that a function is supposed to produce
- Development cycle (red, green, refactor):
    - Write the test
    - Write an empty function template
    - Test that the test fails
    - Program until the test passes
    - Perhaps refactor
    - Move on

---

## Functionality regression tests

- The past is what we accept as correct ([Testing and Continuous Integration with Python](http://katyhuff.github.io/python-testing/))
- If a defect in car engine is fixed, then regression tests can be used to check if the fixed defect has caused any new problems
- Typically tests entire code for a set of input examples and compares them with reference outputs
- Hopefully with numerical tolerance
- Typically we need both unit and functionality regression tests
- Both are no guarantee that the code is correct "always"

Tests are no guarantee ([@dave1010](https://twitter.com/dave1010/status/613601365529657344)):

<img src="{{ site.baseurl }}/img/unit-testing.jpg" style="width: 500px;"/>

---

## Performance regression tests

- Real example
    - In one code module somebody forgot and committed debug code
    - This did not break functionality
    - It slowed down that part of the code by factor 2
    - Nobody noticed for one year because we had no automatic detection of performance degradation

- Good idea
    - Create benchmark calculations to cover various performance-critical modules
    - Run these benchmarks regularly (weekly?)
    - Monitor the timing
    - If timing changes significantly, alarm bells should be ringing

---

## Code coverage

- If I break the code and all tests pass who is to blame?
- A code that is not tested will break sooner or later
- Code coverage measures and documents which lines of code have been traversed during a test run
- It is possible to have line-by-line coverage (example later)
- In all the files that have zero coverage you can multiply all numbers with 10E5 and all tests
  will happily pass

---

## Total time to test matters

- You should require developers to run the test set before each `git push`
- Professional projects require running the test set before each commit
- In extreme cases after each save
- With a `pre-commit` hook you can make sure that commits that break tests are rejected
- Total time to test matters
- If the test set takes 7 hours to run, it is likely that nobody will run it
- Identify fast essential test set that has sufficient coverage and is sufficiently
  short to be run before each commit or push

---

## Continuous integration

- Test each commit (push) on every branch
- Makes it possible for the mainline maintainer to see whether a modification
  breaks functionality before accepting the merge

---

## Good practices

- Test before committing (use the Git staging area)
  - In large projects at least run unit tests for things you have touched
- Fix broken tests immediately (broken windows effect)
- Do not deactivate tests "temporarily"
- Think about coverage (physics and lines of code)
- Go public with your testing dashboard and issues/tickets
- Dogfooding: use the code/scripts that you ship
- Think about input sanitization (green testing dashboard does not prevent me from making unexpected keyword combinations)
- Test controlled errors: if something is expected to fail, test for that
- Make testing easy to run (`make test`)
- Make testing easy to analyze
    - Do not flood screen with pages of output in case everything runs OK
    - Test with numerical tolerance (extremely annoying to compare digits by eye)

## Observe and fix first test

The repository contains the following structure

```
cr-ide-test/
  swissutil/
    __init__.py
    caesar_cipher.py
    math.py
    password_quality.py
  tests/
    __init__.py
    test_caesar_cipher.py
    test_math.py
    test_password_quality.py
```
Let us first focus on math.py and the factorial function there.

Find out how to run all the unit tests using PyCharm (use the find action
feature if necessary. Observe that there are multiple tests in the project and
that they all pass.

Now let's break the tests. Try to add a line and assert that the outpuf of
computing factorial for -1 is sensible. It won't be and in fact the system
will fail.

Find out what causes it to fail by setting a break point. and stepping into
the function that is being tested.

Once you have identified the issue, fix it and commit the result.
