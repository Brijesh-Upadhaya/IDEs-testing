---
layout: episode
title: "Exercise: Testing with pytest"
teaching: 0
exercises: 45
questions:
  - "How can we implement a test suite using pytest?"
  - "I am a Fortran developer, do I need to care about pytest?"
objectives:
  - "Get comfortable with pytest."
---

## Motivation

Most developers start working by contributing to existing projects. The toy
project in this exercise is designed to be 

## Check out repository and set up prerequisites

Clone the project at https://github.com/coderefinery/to-be-determined .

Either use the [VirtualEnv [7]]({{site.baseurl}}/03-features/#virtualenv-7)
feature to create a virtual enviroment or just install the libraries needed in
this example to your global python installation using `pip`.

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

Once you have identified the issue, fix it, *create a branch* and commit the
result result using the built-in VCS system.

## Enable Travis

If you weren't working on a fork you'd have to do the following but now we're
working on a fork.

### (Example, not needed) Enable this repository on [Travis CI](https://travis-ci.org) and
[Coveralls](https://coveralls.io)

On [Travis CI](https://travis-ci.org):

- Use "Sign in with GitHub"
- Click on the little "+" symbol
- Enable the newly created repository for testing (you may need to "Sync
  account" if you do not see it there)

On [Coveralls](https://coveralls.io):

- Use "GITHUB SIGN IN"
- Select "+" symbol: "ADD REPOS" ("SYNC REPOS" if it is not in the list;
  syncing can take a minute)
- If syncing takes forever, reload the page
- Enable the new repository

### (Needed) Create a travis.yml

Add a file `.travis.yml` (mind the "." at the beginning) containing:

```yaml
sudo: false

language:
  - python

python:
  - 2.6
  - 2.7
  - 3.4
  - 3.5

install:
  - pip install pytest pytest-cov python-coveralls

script:
  - if [[ $TRAVIS_PYTHON_VERSION == 2.7 ]];
    then py.test -vv example.py --cov example;
    else py.test -vv example.py;
    fi

after_success:
  - if [[ $TRAVIS_PYTHON_VERSION == 2.7 ]];
    then coveralls;
    fi

notifications:
  email: false
```

Commit changes via the UI.


### Create a fork

Now create your own fork of the repository, add that fork as a remote and push
your feature branch. Create a pull request to the main repository master
branch. Firsst one will have their pull request merged :)

### Update your master

Check out your master branch and pull from origin to reflect the new changes.

### Observe the password_quality.py module

Take a look at the password quality module. There are several things wrong with it:

1. The function name `evaluate_string_for_stuff` is not informative
2. The variable name `foobar` in same function isn't informative either
3. The is_acceptable_input has some semi-cryptic oneliners and one of them has does not do exactly what is intended. Try testing for a password with upper and lower case characters but no numbers
4. `evaluate_string_for_stuff` prints things to standard output, which is a bad practice


Do the following:

1. Use the refactoring features to refactor the names `evaluate_string_for_stuff` and `foobar` to something more sensible.
2. Fix the bug
3. Remove the parts fo evaluate_string_for
