---
layout: episode
title: "Exercise: Testing with pytest"
teaching: 0
exercises: 45
questions:
  - "How does testing work in practice?"
  - "I use vi/emacs/jed, why should I IDE?"
  - "Should I trust a code that has some tests?"
objectives:
  - "Get comfortable with pytest."
  - "Get comfortable with using an IDE"
  - "Make a lot of pull requests"
keypoints:
  - "IDEs make iterative improvement in testing and refactoring manageable"
  - "Tests do not guarantee a function does what it should"
  - "If you encounter a bug, make a test that reproduces it and then fix the
    bug"
---

## Motivation

Most developers start working by contributing to existing projects. The toy
project in this exercise is designed to be a barebones minimal of an open
source project.

## Check out repository and set up prerequisites

Clone the project at https://github.com/coderefinery/cr-ide-test .

**EDIT: pytest and mock are already part of your Anacoda, pytest-mock is not. Skip the below if you already
have Anacoda installed**

Either use the [VirtualEnv [7]]({{site.baseurl}}/03-features/#virtualenv-7)
feature to create a virtual enviroment or just install the libraries needed in
this example to your global python installation using `pip install --user`.

You can find the names of the required packages in requirements.txt. This is a
convention for python packages.

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

The structure is one of the two structures [supported by
pytest](http://pytest.readthedocs.io/en/reorganize-docs/new-docs/user/directory_structure.html).
The reason this was chosen that it would enable some test runners to easily
and efficiently run tests against multiple versions of Python. Also, often
tests aren't held to quite the standard of actual code w.r.t. conventions,
style etc.

Let's first focus on math.py and the factorial function there.

Find out how to run all the unit tests using PyCharm (use the find action
feature if necessary. Observe that there are multiple tests in the project and
that they all pass.

Now let's break the tests. Try to add a line and assert that the outpuf of
computing factorial for -1 is sensible. It won't be and in fact the system
will fail.

Use the [Visual Debugger [3]]({{site.baseurl}}/03-features/#visual-debugger-3)
to Find out what causes it to fail by setting a break point. and stepping into
the function that is being tested. The reason may jump at you but try the
debugger anyway.

It may help to split the view between the module to be tested and the test
module.

Once you have identified the issue, fix it, *create a branch* and commit the
result result using the built-in VCS system. Remember to commit a new test or
edit an existing that fails if the bug is re-introduced at a later date.

> ## What was the issue?
>
> The stopping condition didn't take into account that someone could give a
> negative number to a factorial function. Defining factorials for negative
> numbers is iffy at best. A simple solution would be to return a predefined
> value like 0 or -1. That would create the issue that a factorial function
> would return values that are not in fact valid values for a factorial. A more pythonic way
> would be to raise a ValueError.
>
> {: .solution :}
{: .challenge :}


### Create a fork

Now create your own fork of the repository, add that fork as a remote and push
your feature branch to your fork. Create a pull request to the main repository
master branch. All the concepts should be familiar but now the trick is to
find how to do that in an IDE.

### Update your master

Check out your master branch and pull from origin to reflect the new changes.

In this exercise all the branches were mutually exclusive and your changes are
no longer relevant to the main method. In a normal software development
context having someone just throw your work away and accept someone else's
would merit a temper tantrum but that's the goal of this exercise.

### Take a look at the password_quality.py module

Take a look at the password quality module. There are several things wrong with it:

> ## What is wrong with the module?
> This list is not comprehensive
> 1. The function name `evaluate_string_for_stuff` is not informative
> 2. The variable name `foobar` in same function isn't informative either
> 3. The is_acceptable has some semi-cryptic oneliners and one of them has does not do
>  exactly what is intended. Try testing for a password with upper and lower case characters but no numbers
> 4. `evaluate_string_for_stuff` prints things to standard output, which is a bad practice
>
> {: .solution :}
{: .challenge :}


> ## How to fix/refactor?
> Simple
> 1. Use the refactoring features to refactor the names `evaluate_string_for_stuff` and
>   `foobar` to something more sensible.
> 2. Fix the bug
> 3. Remove the parts of the function formerly known as `evaluate_string_for_stuff`
>   that print things to standard output. Remove the corresponding part from the tests as well.
> 4. (OPTIONAL) If you have the time, re-factor the three tests in `is_acceptable`
>   to separate methods and make a test for each of the methods.
> 5. Again, decide if you want to make one commit or multiple, push to your fork
>   and make a PR
>
> {: .solution :}
{: .challenge :}

While you do these changes you can rapidly iterate by making a change and
running debug. You will probably notice that the refactoring support doesn't
help with e.g. names of functions as mocker parameters.

> ## So why is printing at random places bad?
> Writing to stdout is a so-called *side effect*. If your code has no
> side-effects and is *purely functional*, then we can always replace a
> function call with the return value of said function call.
>
> This makes it considerably easier to write tests. Side-effects also make it
> difficult to reason about what changes to code make, which increases the
> likelihood of so-called *regression bugs* where changes in one part of the
> code break things in another part.
>
> {: .solution :}
{: .challenge :}

### Update your master

Update the master branch after a version of changes have been merged.

## Caesar Ciphers

Caesar ciphers are an ancient way to obfuscate text. To make things a bit
different we use a 30-character alphabet instead of the typical latin 26
character one.

The most important feature of the original rot-13 encryption and this rot-15
toy example is that running the conversion twice gets you the original string.
This is used in the current tests.

However the fact that the software is consistent with itself doesn't mean that
it actually works as intended.

Using the look-up table below make a test to verify that the string "tromsø" is
correctly translated with rot-15. You will find that the method has a bug.

1. Fix the bug
2. (time permitting) implement a rot13 function beside the rot13.
3. (time permitting)  create test(s) for the internal \_lookup function. (The underscore means
   it's supposed to be used internal to the module.)
4. (time permitting) could you refactor the tests for rot13 and rot15 use a
   mock instead of the \_lookup function? should you?
5. Push to your fork and PR

<table width="100%">
  <tr>
    <td>a</td>
    <td>b</td>
    <td>c</td>
    <td>d</td>
    <td>e</td>
    <td>f</td>
    <td>g</td>
    <td>h</td>
    <td>i</td>
    <td>j</td>
    <td>k</td>
    <td>l</td>
    <td>m</td>
    <td>n</td>
    <td>o</td>
    <td>p</td>
    <td>q</td>
    <td>r</td>
    <td>s</td>
    <td>t</td>
    <td>u</td>
    <td>v</td>
    <td>w</td>
    <td>x</td>
    <td>y</td>
    <td>z</td>
    <td>å</td>
    <td>ä</td>
    <td>ö</td>
    <td>ø</td>
  </tr>
  <tr>
    <td>p</td>
    <td>q</td>
    <td>r</td>
    <td>s</td>
    <td>t</td>
    <td>u</td>
    <td>v</td>
    <td>w</td>
    <td>x</td>
    <td>y</td>
    <td>z</td>
    <td>å</td>
    <td>ä</td>
    <td>ö</td>
    <td>ø</td>
    <td>a</td>
    <td>b</td>
    <td>c</td>
    <td>d</td>
    <td>e</td>
    <td>f</td>
    <td>g</td>
    <td>h</td>
    <td>i</td>
    <td>j</td>
    <td>k</td>
    <td>l</td>
    <td>m</td>
    <td>n</td>
    <td>o</td>
  </tr>
</table>
